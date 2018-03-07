# MCNP Walkthrough

Now that you can create and navigate directories, build and save text files, and check cluster availability, you can get started running MCNP simulations. (If you don't know what I'm talking about, go back and start with the [DECF walkthrough](decf_walkthrough.md).)

**Remember that you _cannot_ rucn MCNP on Kepler.**

### MCNP Input Files
First, we need to construct an MCNP input file. I will describe this more in-depth during discussion.

```
Simple Uranium-235 Cube
c cell cards for uranium cube (64cm^3) simulation
1 1 -19.1 -1 2 -3 4 -5 6 	IMP:N=1
2 0      (1:-2:3:-4:5:-6)	IMP:N=0
c end of cell cards for cube simulation

c Beginning of surface
1 px 2	      $ uranium cube (w/ side 4cm)
2 px -2
3 py 2
4 py -2
5 pz 2
6 pz -2
c End of surfaces

M1 92235 1        $ pure uranium-235 [ID ZAID Density]
kcode 10000 1 10 50
ksrc 0 0 0
PRINT 50
```


### MCNP Data

MCNP uses a specific set of data libraries. These are not included in the set of files that your computer searches by default. Instead, you have to add them to this path. The command for this is 

```
setenv DATAPATH /usr/local/mcnp5_lib-160  
```


### MCNP Execution

To run the MCNP input you have created, the command is 

```
mcnp5 inp=cube.inp
```

### MCNP Output

MCNP output will be written to a file named `outp`. (If `outp` already exists, output will be written to a file named `outq`, `outr`, `outs`, or all the way to `out*` where the asterisk will be the next unused letter in the alphabet.)

If you go to the bottom of the output file, you should see a table:

```
              problem        keff     standard deviation       68% confidence         95% confidence         99% confidence

            first half     0.30691         0.00063           0.30627 to 0.30756     0.30558 to 0.30825     0.30508 to 0.30875
           second half     0.30588         0.00052           0.30535 to 0.30641     0.30479 to 0.30697     0.30438 to 0.30738
          final result     0.30640         0.00041           0.30599 to 0.30681     0.30558 to 0.30722     0.30530 to 0.30750

 the first and second half values of k(collision/absorption/track length) appear to be the same at the 95 percent confidence level.

 ***********************************************************************************************************************
```

The key parameter of interest here is the final result for $$k_{\textit{eff}}$$, shown here to be 0.30640. Our uranium cube is clearly not critical.

### Other important concepts

Some important things we will note are:

* Comment cards (`c`) / signs (`$`)
* Macrobodies
* Complement operator `#`
* Elemental vs isotopic ZAID (8000 vs 8016)
* Why are we skipping cycles in KCODE?
* Differences between MCNP/Serpent
	* Largely similar (still have surfaces and cells)
	* No union operator in Serpent (more general shapes)

##### KCODE 

The `KCODE` card indicates that we are performing a criticality calculation. The source size is 10,000 particles, we estimate $$k_{\textit{eff}} = 1.0$$, we skip 10 cycles before averaging $$k_{\textit{eff}}$$, and run a total of 35 cycles (25 are averaged). 


##### KSRC

The initial source location is (0, 0, 0), as specified on the `KSRC` card.

## Outside Resources
[MCNP Primer](http://bl831.als.lbl.gov/~mcfuser/publications/MCNP/MCNP_primer.pdf)


---
[<< DECF Walkthrough](decf_walkthrough.md)

---
title: raser 
use_math: true  
---

**Contents**
* TOC
{:toc}

## Dependences 

- [ROOT](https://root.cern.ch) 
- [Geant4](https://geant4.web.cern.ch)
- [DEVSIM](https://devsim.org/)
- [NGSPICE](https://ngspice.sourceforge.io/)

## Install 

```bash 
pip install raser 
```

## Planner 3D  

- An example python code to use raser:

> $ raser field test-Si-PIN.json

 The output file is in ../raser/output/field/test-Si-PIN

 - example_detector.json(../raser/setting/detectors/test-Si-PIN.json) 
  
```json
[{
    "det_name" : "test-Si-PIN",
    "det_model" : "planar3D",
    "material" : "Si",

    "lx" : 1300,
    "ly" : 1300,
    "lz" : 50,

    "doping":{
        "Acceptors" : "5e12*(step((50e-4)-x)-step(1e-4-x)) + 1.0e18*(step((151e-4)-x)-step((50e-4)-x))",
        "Donors" : "1.0e19*step(1e-4-x)"
    },

    "bias" : {
        "electrode" : "top",
        "voltage" : 200
    },

    "temperature" : 300.0,

    "area_factor" : 1,
    "default_dimension" : 1,

    "mesh" : {
        "1D_mesh" : {
            "mesh_line" : [
                {"pos" : 0,      "ps" : 1e-4, "tag" : "top"},
                {"pos" : 0.5e-4, "ps" : 1e-5, "tag" : "jun_up"},
                {"pos" : 1e-4,   "ps" : 1e-5, "tag" : "mid"},
                {"pos" : 4e-4,   "ps" : 1e-5, "tag" : "jun_down"},
                {"pos" : 150e-4, "ps" : 1e-4, "tag" : "bot"}
            ],
            "region" : [
                {
                    "material" : "Silicon", 
                    "region" : "test-Si-PIN", 
                    "tag1" : "top", 
                    "tag2" : "bot"
                }
            ],
            "contact" : [
                {"name" : "top", "tag" : "top", "material" : "metal"},
                {"name" : "bot", "tag" : "bot", "material" : "metal"}
            ]
        }
    },

    "absorber" : "time_resolution",
    "amplifier" : "BB"
}]
```

##  Timing Resolution Simulation 


```bash 
raser gen_signal test-Si-PIN
```
After generating output files in ../output/gen_signal/test-Si-PIN, run
```bash 
raser timeres test-Si-PIN
```
to generate the result of timing resolution.
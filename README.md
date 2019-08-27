# simpful
A Python library for fuzzy logic reasoning, designed to provide a simple and lightweight API, as close as possible to natural language.

Simpful supports Sugeno reasoning of any order, over arbitrarily complex fuzzy rules involving AND, OR, and NOT operators.

## Usage

```
from simpful import *

# A simple fuzzy model describing how the heating power of a gas burner depends on the oxygen supply.

FR = FuzzyReasoner()

RULE1 = "IF (OXI IS low_flow) THEN (POWER IS LOW_POWER)"
RULE2 = "IF (OXI IS medium_flow) THEN (POWER IS MEDIUM_POWER)"
RULE3 = "IF (OXI IS high_flow) THEN (POWER IS HIGH_POWER)"

FR.set_crisp_output_value("LOW_POWER", 0)
FR.set_crisp_output_value("MEDIUM_POWER", 25)
FR.set_crisp_output_value("HIGH_POWER", 100)

FS_1 = FuzzySet( points=[[0, 1.],  [1., 1.],  [1.5, 0]],          term="low_flow" )
FS_2 = FuzzySet( points=[[0.5, 0], [1.5, 1.], [2.5, 1], [3., 0]], term="medium_flow" )
FS_3 = FuzzySet( points=[[2., 0],  [2.5, 1.], [3., 1.]],          term="high_flow" )
FR.add_membership_function("OXI", MembershipFunction( [FS_1, FS_2, FS_3], 	concept="OXI" ))

FR.add_rules([RULE1, RULE2, RULE3])

# set antecedents values, perform Sugeno inference and print output values
FR.set_variable("OXI", .4)
print FR.Sugeno_inference(['POWER'])
```

## Installation

`pip install simpful`

## Further info
Created by Marco S. Nobile at the Eindhoven University of Technology and Simone Spolaor at the University of Milano-Bicocca. 

If you need further information, please write an e-mail at: m.s.nobile@tue.nl.

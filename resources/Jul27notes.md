#### PyRosetta 3 vs PyRosetta 4

- **PyRosetta 3 is usable only with python2**
- Get PyRosetta 3 Namespace if installing on local machine
- Importing PyRosetta is different in v3 and v4 [more details](https://www.rosettacommons.org/docs/latest/scripting_documentation/PyRosetta/PyRosetta)

~~~
# importing pyrosetta3
from rosetta import *
rosetta.init()

# importing pyrosetta4
from pyrosetta import *
init()
~~~

#### Pose [Unit 2]

- pyrosetta object
- stores protein information (i.e. res, torsion angles)

~~~
# creating a pose object
yourPose = Pose()

# Inserting the sequence in the pose
make_pose_from_sequence(yourPose, "SEQUENCE", "centroid")

# Pose features
yourPose.total_residue()
yourPose.sequence()
yourPose.residue(n) # n is the residue number
yourPose.residue(n).is_protein()

# angles
yourPose.phi(n)
# setting angles
yourPose.set_phi(n, new_angle)

# check pose type
yourPose.is_fullatom()
yourPose.is_centroid()
~~~

#### Score functions [Unit 3]
- Used for evaluating the free energy of your protein
- Varies from protein to protein
- Many preset available
- Literature is the best method to find the most suitable score function

~~~
# initializing your score function
yourScoreFxn = ScoreFunction()

# setting weights to the score function
yourScoreFxn = set_weight(vdw, 1.0)
yourScoreFxn = set_weight(hbond_lr_bb, 1.0)

# checking the score function
print yourScoreFxn

# evaluating a pose with the score function
yourScoreFxn(yourPose)
~~~


#### Monte Carlo Object [Unit 4]

- Stores energy information of the structure for perturbations
- Selects the lowest energy conformation
- Applies that change to the pose

~~~
# initializing
mc = MonteCarlo(yourPose, yourScoreFxn, kT)

# typical for loop for MC
for i in range(i, ncycles):
  yourMover.apply(yourPose)
  mc.boltzmann(yourPose)
  mc.show_scores()
  mc.show_counters()
  mc.show_state()
mc.recover_low(yourPose)
~~~

#### Movers [Unit 5]

- Many types of Movers (i.e. smallmover, shearmover, fragmentmover)
- Specific changes based on phi and psi restrictions in secondary structure (use Ramachandran plot as reference)
- Details in manual

#### Output

~~~
dump_pdb(yourPose, "YOUR/PATH/FOR/OUTPUT/out_pdb_name.pdb")
~~~

#### Researching structures and methods
- Finding papers that have run similar simulations [Papers using rosetta](https://www.rosettacommons.org/about/publications)
- Score functions can be found by searching Literature for similar structures

# This submit a job in bigred2
MPIRUNCMD = srun
LAMMPSEXE = lmp_mpi
JOBSCR = nanoconfinement.pbs
TEST = test.pbs
JOBSCRLMP = nanoconfinement-lammps.pbs
Z=3
p=1
n=-1
c=0.5
d=0.714
a=0.714
i=0.0
S=5000000
NODESIZE=4

submit:
	@echo "Launching the job";
	sbatch $(JOBSCR)

test:
	@echo "Launching the test job for nanoconfinement-md";
	sbatch $(TEST)


run-preprocessor:
	$(MPIRUNCMD) -n 1 md_simulation_confined_ions -Z $(Z) -p $(p) -n $(n) -c $(c) -d $(d) -a $(a) -S $(S) -i $(i) -J true -j true

run-postprocessor:
	$(MPIRUNCMD) -n 1 md_simulation_confined_ions -Z $(Z) -p $(p) -n $(n) -c $(c) -d $(d) -a $(a) -S $(S) -i $(i) -J true -j false

submit-lammps:
	@echo "Launching the job for Lammps script in BIGRED3";
	sbatch $(JOBSCRLMP)

run-local-parallel:
	time $(MPIRUNCMD) -n $(NODESIZE) $(LAMMPSEXE) < in.lammps

run-local-serial:
	time $(LAMMPSEXE) < in.lammps

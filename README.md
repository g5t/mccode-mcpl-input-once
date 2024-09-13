# Alternate MCPL input component for McStas
The original `MCPL_input.comp` MCPL input component is not suitable for use-cases where the runtime is more important
that the simulation fidelity.
When run under MPI, it re-uses the same input particle list for all nodes -- so if the input file has 1M particles
and the MPI setup has 6 nodes, a total of 6M particles will be used independent of any command-line particle-count switch.

This component is intended to be a drop-in replacement, except that it divides the file particles
into approximately equal chunks between MPI nodes. And that `repeat` is removed, in favor of using the user-provided
neutron count; with repeating implied if the requested number exceeds the file's contained particle count.

---
title: Submitting Jobs
nav_order: 3
---

# Submitting Jobs

The cluster uses the Slurm queue management system (stands for Simple Linux Utility for Resource Management) for
scheduling, distributing, and managing compute "jobs". A "job" is just a general term used to describe doing a specific
task, or set of tasks (specified in script) on the compute contained within the cluster.

[Slurm Documentation](https://docs.uabgrid.uab.edu/wiki/Slurm){: .btn .btn-blue }

For a complete description and tutorial of writing and executing jobs on the cluster see Research Computing's helpful
[guide](https://docs.uabgrid.uab.edu/wiki/Slurm) on Slurm and executing compute tasks on the cluster. You can also check
out the below tutorial for a quick high level view of the cluster.

## Multiple Partitions

Tip
{: .label .label-yellow }

You can specify multiple partitions in your Slurm script by listing them separated by commas in the `#SBATCH --partition` directive:

```bash
#SBATCH --partition=partition1,partition2,partition3
```

This allows your job to run on any of the specified partitions, which can help reduce wait times if one partition is busy.

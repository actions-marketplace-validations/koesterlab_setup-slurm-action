# A Github Action for setting up a small slurm cluster

This action utilizes https://github.com/galaxyproject/ansible-slurm for automatically setting up a SLURM cluster for testing purposes.
It can be used in the following way:

```yaml

jobs:
  testing:
    runs-on: ubuntu-latest
    # For the action to work, you have to supply a mysql
    # service as defined below.
    services:
      mysql:
        image: mysql:8.0
        env:
          MYSQL_ROOT_PASSWORD: root
        ports:
          - "8888:3306"
        options: --health-cmd="mysqladmin ping" --health-interval=10s --health-timeout=5s --health-retries=3
    steps:
      - uses: actions/checkout@v3

      - uses: koesterlab/setup-slurm-action@v1

      # Afterwards, you can submit to the slurm cluster via sbatch and srun, 
      # and interact via all other usual commands.
```
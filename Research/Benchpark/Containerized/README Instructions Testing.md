System Configuration:
- Resource: JetStream2
- CPU: 2 Cores
- RAM: 125 GB
- Root Disk: 100 GB
- OS: Rocky Linux 9


```bash
cd benchpark
. setup-env.sh
```

This worked fine.

```bash
benchpark containerize rockylinux:9 openmpi -o benchpark.dockerfile
```

The above command gave me the following error:
```bash
[exouser@benchpark-containerized benchpark]$ benchpark containerize rockylinux:9 openmpi -o benchpark.dockerfile
Cloning Ramble to /home/exouser/.benchpark/ramble
Cloning Spack to /home/exouser/.benchpark/spack
Traceback (most recent call last):
  File "/home/exouser/benchpark/lib/main.py", line 21, in <module>
    import benchpark.cmd.unit_test
  File "/home/exouser/benchpark/lib/benchpark/cmd/unit_test.py", line 8, in <module>
    import pytest
ModuleNotFoundError: No module named 'pytest'
Traceback (most recent call last):
  File "/home/exouser/benchpark/bin/benchpark", line 23, in <module>
    main()
  File "/home/exouser/benchpark/bin/benchpark", line 19, in main
    subprocess.run([sys.executable, main_py] + sys.argv[1:], check=True)
  File "/usr/lib64/python3.9/subprocess.py", line 528, in run
    raise CalledProcessError(retcode, process.args,
subprocess.CalledProcessError: Command '['/usr/bin/python3', PosixPath('/home/exouser/benchpark/lib/main.py'), 'containerize', 'rockylinux:9', 'openmpi', '-o', 'benchpark.dockerfile']' returned non-zero exit status 1.
```

This was fixed by:
```
pip install pytest
```

```bash
docker build -f benchpark.dockerfile -t benchpark_base .
```

This command took 2589 seconds to complete.

```
docker run --rm -it --name benchpark_container benchpark_base
```

```bash
cd benchpark
benchpark system init --dest=oci-system oci
```

This command worked fine.

```bash
benchpark experiment init --dest kripke-test kripke +single_node +openmp
benchpark setup kripke-test/ oci-system/ workspace/
```

This worked fine.

```bash
. /home/jovyan/benchpark/workspace/setup.sh
ramble --disable-progress-bar --workspace-dir /home/jovyan/benchpark/workspace/kripke-test/Oci-ec4b246/workspace workspace setup
ramble --disable-progress-bar --workspace-dir /home/jovyan/benchpark/workspace/kripke-test/Oci-ec4b246/workspace on
```

This caused me an issue where Kripke doesn't seem to execute properly and ends prematurely:
This is the only standard output i get:  

```
[jovyan@037527017e25 benchpark]$ ramble --disable-progress-bar --workspace-dir /home/jovyan/benchpark/workspace/kripke-test/Oci-ec4b246/workspace on
==> Streaming details to log:
==>   /home/jovyan/benchpark/workspace/kripke-test/Oci-ec4b246/workspace/logs/execute.2024-12-13_17.10.00.out
==>   Executing 1 out of 1 experiments:
==>   Log files for experiments are stored in: /home/jovyan/benchpark/workspace/kripke-test/Oci-ec4b246/workspace/logs/execute.2024-12-13_17.10.00
==> Running executors...
```

With regards to the log files:  

```
[jovyan@037527017e25 benchpark]$ cat /home/jovyan/benchpark/workspace/kripke-test/Oci-ec4b246/workspace/logs/execute.2024-12-13_17.10.00.out
==>   Log files for experiments are stored in: /home/jovyan/benchpark/workspace/kripke-test/Oci-ec4b246/workspace/logs/execute.2024-12-13_17.10.00
==> Running executors...
```

```
[jovyan@037527017e25 benchpark]$ cat /home/jovyan/benchpark/workspace/kripke-test/Oci-ec4b246/workspace/logs/execute.2024-12-13_17.10.00/kripke.kripke.kripke_kripke_single_node_openmp_64_1_128_128_4_2_2_1_64_64_32_4_1.out 
==>     Using default usage mode standard on modifier allocation
==> Phase timing statistics:
==>     Using default usage mode standard on modifier allocation
```



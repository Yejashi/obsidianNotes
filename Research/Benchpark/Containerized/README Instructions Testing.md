System Configuration:
- Resource: JetStream2
- CPU: 2 Cores
- RAM: 120 GB
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



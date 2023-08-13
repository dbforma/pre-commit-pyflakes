#!/usr/bin/env python3

import subprocess
import sys


def main():
    print("Running hook-pyflakes.py...")

    find_cmd = "find $PWD -type d -name '.env' -prune -o -type f -name '*.py' -print"
    xargs_cmd = "xargs pyflakes"

    proc_find = subprocess.Popen(
        args=find_cmd,
        stdout=subprocess.PIPE,
        stderr=subprocess.PIPE,
        shell=True,
    )
    stdout_find, _ = proc_find.communicate()

    proc_xargs = subprocess.Popen(
        args=xargs_cmd,
        stdin=subprocess.PIPE,
        stdout=subprocess.PIPE,
        stderr=subprocess.PIPE,
        shell=True,
    )
    stdout_xargs, stderr_xargs = proc_xargs.communicate(stdout_find)

    if proc_xargs.returncode:
        print("[INFO] Pyflakes found some violations. Please fix them or force the commit with --no-verify")
        print(stdout_xargs.decode())
        sys.exit(proc_xargs.returncode)


if __name__ == '__main__':
    main()

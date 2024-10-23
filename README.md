# adroit_symlink_ondemand

```bash
#!/bin/bash

cd $HOME
ls -la > /scratch/rapids/$USER.log

if [ -h .conda ]; then
    if [ "$(readlink -- .conda)" = /scratch/network/tx/.conda/ ]; then
        echo ""
        echo "Success! You are ready for the workshop."
        echo ""
        exit
    fi
fi

if [ -e .conda ]; then
    mv .conda .conda_MOVED
    echo "Found .conda and moved it to .conda_MOVED. After the workshop you will"
    echo "need to run these commands:"
    echo ""
    echo "    $ rm ~/.conda"
    echo "    $ mv ~/.conda_MOVED ~/.conda"
    ln -s /scratch/network/tx/.conda/ .conda
    echo ""
    echo "Created symbolic link."
else
    ln -s /scratch/network/tx/.conda/ .conda
    echo ""
    echo "Created symbolic link."
    echo ""
    echo "After the workshop you should run this command:"
    echo ""
    echo "    $ rm ~/.conda"
fi

if [ "$(readlink -- .conda)" = /scratch/network/tx/.conda/ ]; then
    echo ""
    echo "Success! You are ready for the workshop."
else
    echo "Something went wrong. You are not ready for the workshop."
fi
```

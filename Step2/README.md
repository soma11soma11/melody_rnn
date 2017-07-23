# Magenta Melody RNN

## Getting Started

* [Installation](#installation)
* [Using Magenta](#using-magenta)
* [Playing a MIDI Instrument](#playing-a-midi-instrument)
* [Development Environment (Advanced)](#development-environment)

## Installation

### Python Pip

Magenta maintains a [pip package](https://pypi.python.org/pypi/magenta) for easy
installation. We recommend using Anaconda to install it, but it can work in any
standard Python 2.7 environment. These instructions will assume you are using
Anaconda.

Note that there are additional instructions below if you want to enable GPU support.

#### Automated Install

If you are running Mac OS X or Ubuntu, you can try using our automated
installation script. Just paste the following command into your terminal.

```
curl https://raw.githubusercontent.com/tensorflow/magenta/master/magenta/tools/magenta-install.sh > /tmp/magenta-install.sh
bash /tmp/magenta-install.sh
```

After the script completes, open a new terminal window so the environment
variable changes take effect.

The Magenta libraries are now available for use within Python programs and
Jupyter notebooks, and the Magenta scripts are installed in your path!

Note that you will need to run `source activate magenta` to use Magenta every
time you open a new terminal window.

#### Manual Install

If the automated script fails for any reason, or you'd prefer to install by
hand, do the following steps.

First, download the
[Python 2.7 Miniconda installer](http://conda.pydata.org/miniconda.html) (you
can skip this step if you already have any variant of conda installed).

Next, create and activate a Magenta conda environment using Python 2.7 with
Jupyter notebook support:

```
conda create -n magenta python=2.7 jupyter
source activate magenta
```

Install the Magenta pip package:

```
pip install magenta
```

The Magenta libraries are now available for use within Python programs and
Jupyter notebooks, and the Magenta scripts are installed in your path!

Note that you will need to run `source activate magenta` to use Magenta every
time you open a new terminal window.

#### GPU Support

If you have a GPU installed and you want Magenta to use it, there are some additional
steps to take after you've installed the pip package (using either the automated
install or the manual install above).

First, make sure your system meets the [requirements to run tensorflow with GPU support](
https://www.tensorflow.org/install/install_linux#nvidia_requirements_to_run_tensorflow_with_gpu_support).

Next, activate your `magenta` environment and install the `tensorflow-gpu` pip package:

```
source activate magenta
pip install tensorflow-gpu
```

Magenta should now have access to your GPU.

### Docker
Another way to try out Magenta is to use our Docker container.
First, [install Docker](https://docs.docker.com/engine/installation/). Next, run
this command:

```
docker run -it -p 6006:6006 -v /tmp/magenta:/magenta-data tensorflow/magenta
```

This will start a shell in a directory with all Magenta components compiled,
installed, and ready to run. It will also map port 6006 of the host machine to
the container so you can view TensorBoard servers that run within the container.

This also maps the directory `/tmp/magenta` on the host machine to
`/magenta-data` within the Docker session. Windows users can change
`/tmp/magenta` to a path such as `C:/magenta`, and Mac and Linux users
can use a path relative to their home folder such as `~/magenta`.
**WARNING**: only data saved in `/magenta-data` will persist across Docker
sessions.

The Docker image also includes several pre-trained models in
`/magenta/models`. For example, to generate some MIDI files using the
[Lookback Melody RNN](magenta/models/melody_rnn#lookback), run this command:

```
melody_rnn_generate \
  --config=lookback_rnn \
  --bundle_file=/magenta-models/lookback_rnn.mag \
  --output_dir=/magenta-data/lookback_rnn/generated \
  --num_outputs=10 \
  --num_steps=128 \
  --primer_melody="[60]"
```

**NOTE**: Verify that the `--output_dir` path matches the path you
mapped as your shared folder when running the `docker run` command. This
example command presupposes that you are using `/magenta-data` as your
shared folder from the example `docker run` command above.

One downside to the Docker container is that it is isolated from the host. If
you want to listen to a generated MIDI file, you'll need to copy it to the host
machine. Similarly, because our
[MIDI instrument interface](magenta/interfaces/midi) requires access to the host
MIDI port, it will not work within the Docker container. You'll need to use the
full Development Environment.

You may find at some point after installation that we have released a new version of Magenta and your Docker image is out of date. To update the image to the latest version, run:

```
docker pull tensorflow/magenta
```

Note: Our Docker image is also available at `gcr.io/tensorflow/magenta`.

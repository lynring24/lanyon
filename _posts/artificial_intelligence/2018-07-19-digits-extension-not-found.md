Digits Plugin Extension Problem

Path was the problem so had to import sys to get the absolute path.

{% highlight python %}
import os, sys
from setuptools import setup, find_packages
grand_Path = os.path.abspath($CAFFE_ROOT)

if grand_Path not in sys.path:
    sys.path.insert(0, grand_Path)

from digits.extensions.data import GROUP as DIGITS_PLUGIN_GROUP

# Utility function to read the README file.
def read(fname):
    return open(os.path.join(os.path.dirname(__file__), fname)).read()

setup(
    name="digits_text_classification_data_plugin",
    version="0.0.1",
    author="Greg Heinrich",
    description=("A data ingestion plugin for text classification"),
    long_description=read('README'),
    license="BSD",
    packages=find_packages(),
    entry_points={
        DIGITS_PLUGIN_GROUP: [
            'class=digitsDataPluginTextClassification:DataIngestion',
        ]},
    include_package_data=True,
)
{% endhighlight %}

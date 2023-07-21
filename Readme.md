<h2 align="center">
  Markdown Example for sdRDM
</h2>

<p align="center">
This is an example of how to set up a data model using the Software-Driven Research Data Management (sdRDM) library based on abstract object models. Furthermore, the sdRDM library supports the conversion of data models defined in the Markdown format.</p>

### ✍️ Syntax

Data models defined in the Markdown format follow these conventions:

- **Modules** are denoted by a heading level 1 ```#```
- **Structural** headings are denoted by a heading level 2 ```##``` and can be used to structure your document.
- **Objects** are started with a heading level 3 ```###```
- Each object contains **fields** as a list &rarr; ```- name```
- **Required fields** are denoted in bold &rarr; ```- __name__```
- Each field has **options** as a list of name to value mapping &rarr; ```- Type: string```

### ⚙️ Field options

Each field in an object can hold options relevant for mapping to another data model (e.g. a standardized format) and general information such as its type and description. In the following is a collection of all native and required fields:

- **Type** - Required option to denote the data type. Just so you know, this can also include other objects defined in this document.
- **Multiple** - Whether or not this field can contain multiple values. Setting to ```True```will result in a ```List[dtype]```annotation in the software.
- **Description** - Required option to describe the field. This should be a brief description that explains what the attribute is about.

### 🧬 Inheritance

To inherit attributes to another object, the object definition additionally includes the name of the parent object in italic wrapped with brackets:

&rarr; ```## Child [_Parent_]```

In the following, an [example](https://github.com/JR-1991/sdrdm-template/tree/main/specifications) data model is defined using the above rules. You can also use this example as a template for your application.

### 👁 How can I use it by myself?

You can experiment and use this [example](https://github.com/JR-1991/sdrdm-template/tree/main/specifications) repository right away to get familiar with the concept. This repository includes an [action](https://github.com/JR-1991/sdrdm-template/blob/main/.github/workflows/generate_api.yaml) triggered whenever changes are pushed. Thus, when you introduce changes to the markdown document, these will be reflected directly onto the generated software. Follow these steps to start:

#### 👋 One thing, before you start

The sdRDM library is still under active development and will be released soon. For now, you can use the development version by installing it from GitHub using the following command:

```bash
python3 -m pip install git+https://github.com/JR-1991/software-driven-rdm.git@linking-refactor
```

1. Fork this repository into your profile. This will create an exact copy, but you can modify it without affecting the original.

<center>
  <img src="https://www.earthdatascience.org/images/earth-analytics/git-version-control/githubguides-bootcamp-fork.png" width="500" />
</center>

2. Open the ```specifications/Example.md``` file and edit it according to the syntax. You can also press ```Preview``` to inspect the rendered Markdown.

<center>
  <img src="https://docs.github.com/assets/cb-118903/images/help/repository/edit-file-edit-dropdown.png" width="500" />
</center>

3. Commit changes to the ```main``` branch or create a new one. By creating a new branch, you can safely work without affecting the original. Once your modifications are done, you can merge these into the ```main``` branch.

<center>
  <img src="https://docs.github.com/assets/cb-32137/images/help/repository/choose-commit-branch.png" width="500" />
</center>

4. Watch your changes being reflected in the API. You can also directly fetch this model using the [sdRDM](https://github.com/JR-1991/software-driven-rdm) library. For this, you can use the following example code that should run as is.

```python
from sdRDM import DataModel

lib = DataModel.from_git(
    url="https://github.com/JR-1991/sdrdm-template.git",
)

# Visualize the data model
lib.Root.meta_tree()

# Enter your data
dataset = lib.Root(title="Some Title", description="Some Description")

# There are add-functions generated with whom you are able to add
# objects to your dataset. These functions are named after the object
# they are adding to and are prefixed with "add_to_". The add-function
# will return the object that was added to the dataset. You can use this
# object to add further objects to it or manipulate it in any other way.

author = dataset.add_to_authors(name="Jan Range", affiliation="SimTech")
parameter = dataset.add_to_parameters(key="Param", value=10.0)

# Inspect your dataset
print(dataset.yaml())

# Option: Export your dataset to another format
with open("my_dataset.json", "w") as f:
    f.write(dataset.json())

# Re-opening your dataset using sdRDM will cause the library
# to re-build the software state in which the dataset was created

```

### 🧃 Using the GitHub Action

The workflow included in this repository synchronizes the software to the markdown document. Thus, if you extend or change your data model, it will be immediately usable. This also works for Pull Requests and other branches. So feel free to experiment around! Furthermore, the action creates a UML digram within the API `schemes` directory.

*(Images were taken from GitHub's ["Editing Files" tutorial](https://docs.github.com/en/repositories/working-with-files/managing-files/editing-files))*

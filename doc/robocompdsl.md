#Using robocompdsl: the command line component generator

**robocompdsl** is the new tool used in RoboComp to automatically generate components and modify their main properties once they have been generated (e.g., communication requirements, UI type). It is one of the core tools of the framework so, if you installed RoboComp, you can start using it right away.

This new version can only be used from the command line, but the languages used to define components and their interfaces remain mostly the same: **CDSL** to specify components and **IDSL** to specify interfaces. The only difference with the old RoboCompDSLEditor tool is that the reserved keywords (are now case independent). Take a look to the tutorial ["a brief introduction to Components"](components.md) for an introduction to the concept of component generation and the languages involved.

There are three tasks we can acomplish using **robocompdsl**: 

* generating a CDSL template file
* generating the code for a previously existing CDSL file
* regenerating the code for an already generated component.

## Generating a CDSL template file
Even tough writing CDSL files is easy --their structure is simple and the number of reserved words is very limited-- robocompdsl can generate template CDSL files to be used as a guide when writing CDSL files.

    $ robocompdsl path/to/mycomponent/mycomponent.cdsl

This will generate a CDSL file with the following content:

    import "/robocomp/interfaces/IDSLs/import1.idsl";
    import "/robocomp/interfaces/IDSLs/import2.idsl";
 
    Component CHANGETHECOMPONENTNAME
    {
    	Communications
    	{
    		implements interfaceName;
    		requires otherName;
    		subscribesTo topicToSubscribeTo;
    		publishes topicToPublish;
    	};
    	language Cpp;
    	gui Qt(QWidget);
    };

The CDSL language is described in the tutorial ["A brief introduction to Components"](components.md). Just don't forget to change the name of the component.

 
## Generating a component given a CDSL file
Once we have our CDSL file we can generate the component's source code running robocompdsl with the CDSL file as first argument and the directory where the code should be placed as the second argument.

From the component's directory:
    $ cd path/to/mycomponent
    $ robocompdsl mycomponent.cdsl .

Or somewhere else:
    $ robocompdsl path/to/mycomponent/mycomponent.cdsl path/to/mycomponent

These commands will generate the C++ or Python code in the specified directory.


## Updating the source code of a component after modifying its CDSL file
Once we generated our component we might change our mind and decide to add a new connection to another interface or to publish a new topic. In these cases we can regenerate the code of the component just by changing the *.cdsl* file and executing again the command.

As you might have learned from the tutorial ["A brief introduction to Components"](components.md) RoboComp components are divided in specific code (files where you write your code) and generic code (autogenerated code which doesn't need to be edited). Running robocompdsl again on the same directory will ony overwrite these generic files. To ensure robocompdsl doesn't overwrite the changes you made to the specific files these are left unchanged, so the component might not compile after regeneration (e.g., you might need to add new methods).






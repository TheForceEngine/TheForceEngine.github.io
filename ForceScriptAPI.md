---
layout: default
title: Force Script C++ API
permalink: TFE_ForceScriptAPI.html
---
### Script API
For TFE, scripts interface with the system using simplified "API" classes. The classes are defined by the engine, scripts call functions and access member variables. It is intended that the script API does **not** match one to one with the game or engine classes and structures. It should be streamlined and be robust against internal C++ refactoring and changes. Each script class defines an API through which scripts interface with the engine and game.

Example script - get level information in the editor:
```
void main()
{
	string name = level.getName();
	string slot = level.getSlot();
	int sectorCount = level.getSectorCount();
	int entityCount = level.getEntityCount();
}
```

Notice that the script is using the **Level** API through the **level** instance defined by the engine. Note that it is possible to define types and structures in C++ that scripts can use, that will be covered later.

### Creating a script API Class
These are standard C++ classes with a few caveats:
* Only one instance will be created.
* It must derive from the ScriptAPI class.
* It must override the scriptRegister() function.

```
class MyClass : public ScriptAPIClass
{
public:
  // Functions and stuff
  bool scriptRegister(ScriptAPI api) override;
}
```

The most interesting part is the `scriptRegister() function`. The script class is defined using ScriptClassBegin() and ScriptClassEnd():
```
bool MyClass::scriptRegister(ScriptAPI api)
{
	ScriptClassBegin("MyClass", "myClass", api);
	{
		// Interface registration for the class goes here.
	}
	return ScriptClassEnd();
}
```
Where "MyClass" is the name of the API in the script and "myClass" is the global instance that the script will use to access the API: `myClass.someFunc();`, "api" defines which ScriptAPI this API will be available through. For example, level editor APIs will not be accessible from game scripts due to differences in internal structures. ScriptClassEnd() returns true if the setup was successful, otherwise it will be false. In debug an assert will fire on failure.

Next you will need to expose enums, class member functions, member variables, and so forth to the script API.

### Defining Enums
Enumerations can be defined in two different ways - one where the C++ and script names match and the other where they can be different.

Names match:
```
ScriptEnumRegister("EnumName");
ScriptEnumStr(WP_MID);
ScriptEnumStr(WP_TOP);
ScriptEnumStr(WP_BOT);
ScriptEnumStr(WP_SIGN);
```
Here the values are from the C++ enum and those same names will be used by scripts.

Names are different:
```
ScriptEnumRegister("SectorFlags1");
ScriptEnum("SECTOR_FLAG1_EXTERIOR", SEC_FLAGS1_EXTERIOR);
ScriptEnum("SECTOR_FLAG1_DOOR",     SEC_FLAGS1_DOOR);
ScriptEnum("SECTOR_FLAG1_MAG_SEAL", SEC_FLAGS1_MAG_SEAL);
...
```
Here the string is the name is the script API and the values is the C++ enum value.

### Member Functions
Member functions are members of the C++ class. When using these all of the class member variables will be available.
```
ScriptObjMethod(Declaration, function)
```
The declaration is the **Script** declaration (const char* string) and the function is simply the function name (not a string, the function name itself). Examples:
```
ScriptObjMethod("void findSector(const string &in)", findSector);
ScriptObjMethod("void findSectorById(int)",          findSectorById);
```
* **string** is a `std::string`.
* **float2** is the Force Script built-in float2 type, use `Vec2f_to_float2()` and `float2_to_Vec2f` to convert to and from the TFE engine Vec2f type.
* Other basic types include int, float, bool - which map to s32, f32, bool, etc.

### Lambda Functions
Sometimes the script API Class is a wrapper around other systems and functionality. In this case, it is easier to embed the access code directly into the interface definition. When using lambda functionality, *this* is not available, but otherwise normal C++ functionality is.

```
ScriptLambdaMethod(Declaration, (Argument List), Return Type, { function body })
```
The declaration is the **Script** declaration, just like normal methods. The Argument list is the **named** list of arguments that will be passed to the lambda from the script. The Return type is the return type, which can be void. Finally the function body is a normal C++ function, but should be kept short - if a longer function is needed, then a member function is preferred.

Examples:
```
ScriptLambdaMethod("string getName()", (), std::string, { return s_level.name; });

ScriptLambdaMethod("string getSlot()", (), std::string, { return s_level.slot; });

ScriptLambdaMethod("void setName(const string &in)", (std::string& name), void, { s_level.name = name; });

ScriptLambdaMethod("void setPalette(const string &in)", (std::string& palette), void, { s_level.palette = palette; });
```
Notice that if no arguments are needed **()** should be used. Also, notice that getters and setters can be implemented in this way. In this case **s_level** is the level data used by the Level Editor.

### Member Variables
Exposing class member variables allows them to be read and written to by scripts. If specific access control is needed, or if the variables are wrapping game/engine variables directly then **Accessors** should be used instead (see below).

`TODO`

### Accessors
Accessors allow more controlled access to variables. In the script, it will look like direct access to member variables, but on the C++ side read/write can be controlled, and non-member variables can be wrapped to avoid extra boilerplate.

`TODO`

# Rules #

## Basic Rules ##
| Classname | Description |
|:----------|:------------|
| com.googlecode.japi.checker.rules.AllRules | Wrapper rules which enables all the following  rules. |
| com.googlecode.japi.checker.rules.CheckChangeOfScope | Check if the visibility of any public or protected class/method/field has been lowered.  |
| com.googlecode.japi.checker.rules.CheckClassVersion | Check if a class has been compiled for a different target platform (e.g: reference is compiled for 1.3 and new version is 1.6).  |
| com.googlecode.japi.checker.rules.CheckFieldChangeOfType | check that a public/protected field has still the same type.  |
|com.googlecode.japi.checker.rules.CheckFieldChangeToStatic| Checks if a public/protected field has been un/made static. |
| com.googlecode.japi.checker.rules.CheckInheritanceChanges| Checks if an visible class still derive the same class, and implements the same set of interfaces (implementing more is not a problem). |
|com.googlecode.japi.checker.rules.CheckMethodExceptions|Validates that a methods still throw compatible exeptions. |
|com.googlecode.japi.checker.rules.CheckRemovedField|Checks that class public/protected fields are not removed.|
|com.googlecode.japi.checker.rules.CheckRemovedMethod|Checks that class public/protected methods are not removed.|
|com.googlecode.japi.checker.rules.ClassChangedToAbstract|Check if any visible classes have been made abstract. |
|com.googlecode.japi.checker.rules.ClassChangedToFinal|Checks if any visible classes have been made final. This breaks inheritance of extending classes. |
|com.googlecode.japi.checker.rules.ClassChangedToInterface|Checks if a class nature has been changed  from regular class to interface. |
|com.googlecode.japi.checker.rules.CheckMethodChangedToFinal|Checks if a method has been made final. This prevents overriding. |
|com.googlecode.japi.checker.rules.InterfaceChangedToClass|Checks if a class nature has been changed  from interface to a regular class.|
|com.googlecode.japi.checker.rules.CheckSuperClass|Checks if the base class of a class remains backward compatible. This allows you to change the base class as long as the base class itself inherits from the previous base class. |

## JSR305 Rules ##

| Classname | Description |
|:----------|:------------|
|com.googlecode.japi.checker.rules.CheckJSR305|Checks contract changes regarding the Nonnull and Nullable annotations. |
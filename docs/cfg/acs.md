# ACS System
***

## About

WWIV now supports a simple expression language for supporting 
a basic Access Control System (ACS) to allow more fine grained
access primitives for users on the BBS.

WWIV's ACS suppors the following objects:

| Name    | Description |
| ------- | ----------- |
| User    | Provides attributes about the current user
| System  | Provides attributes about the bbs


## Syntax

The ACS language allows conditional attribute-based access control for WWIV BBS system
resources, such as message areas, conferences, file areas, chains, and menu items.  
This allows the system to specify the conditions in a free-form DSL language that
determines if access is granted.

### Language Elements

WWIV's ACS grammar is comprised of:

* Object Attributes
* Comparison Operators
* Logical Operators
* Object Attributes
* Expressions 

#### Data Types

ACS support the following datatypes:

* Number (an integer value of 32 bits in size)
* String (a variable length set of CP437 characters)
* Boolean (support either true of false)
* ACSSet (contains the set of ACS values, supports equality checks against single 
  ACS value specified as a string.)

#### Object Attributes
WWIV ACS supports attributes in the form 
Object.Attribute. For example "user.sl" is the current user's security level.<br>
*Note:* Object and attribute names are case-insensitive, so 
both ```user.name``` and ```USER.NAME``` are equivalent.

#### Operators
    OP ::= COMPARE_OP | LOGICAL_OP

Only Binary Operators are supported in ACS.  The operators may be either a comparison
operator or a logical operator.

##### Comparison Operators
		LHS COMPARE_OP RHS


Comparison Operators are binary operators that compare the values of both operands and
return a true or false boolean value.

WWIV ACS supports the following Comparison Operators with ```LHS``` as the Left
Hand Side operand and ```RHS``` as the right hand side operand:

| Name                  | Symbol   | Description
| --------------------- | -------- | -----------
| Greater Than          | ```>```  | True if LHS > RHS
| Greater Than or Equal | ```>=``` | True if LHS >= RHS
| Less Than             | ```<```  | True if LHS < RHS
| Less Than or Equal    | ```<=``` | True if LHS <= RHS
| Equal                 | ```==``` | True if LHS == RHS
| Not Equal             | ```!=``` | True if LHS != RHS
 
 <br/>

Example:

      user.sl > 100


##### Logical Operators
		LHS LOGICAL_OP RHS

The name logical comes from boolean logic, although the operands on either side of
the operator may be an expression or type that evaluates independently to a boolean.

WWIV ACS supports the following Logical Operators:

| Name | Symbol | Description
| ---- | ------ | -----------
|  AND | ```&&``` | Both operands must evaluate to true for the result to be true.
|  OR  | ```||``` | At least one operand must evaluate to true for the result to be true.

<br/>

Example:

      user.sl > 100 || user.ar == 'A'


#### Expression
    OP ::= COMPARE_OP | LOGICAL_OP
		EXPRESSION ::= EXPRESSION (OP EXPRESSION)?

The language is designed to evaluate a single expression.  An expression may be
a compound expression with multiple expressions combined using logical 
AND ```&&``` or OR ```||``` operators.



## Examples

Grant access to  users with SL of 100 or more or AR of 'A':
      
      user.sl >= 100 || user.ar == 'A'

Grant access to users with SL of 20 or less, and also to Rushfan.
      
      user.sl <= 20 || user.name == "Rushfan"
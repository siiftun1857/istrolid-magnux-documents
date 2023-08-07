# Istrolid game server API
## playerJoin
**pid**:  
integer number

**name**:  
string  
must be equal to the name value from playerValid

**color**:  
Array with 4 element  
element 0 1 2 must be integer number in 0~255  
element 3 must be 255

**buildBar**:  
Array with 10 elements  
element must be null or string

**aiRules**:  
null or Array with 10 elements  
element must be null or Array

**ai**:  
must be false

**update**:  
true or false

## gameKey
**name**:  
string

**gamekey**:  
string

## mouseMove
**pos**:  
Array with 2 elements  
elements must be number

**action**:  
true or false

## playerSelected
**selection**:  
Array  
elements must be integer number

## setRallyPoint
**point**:  
Array with 2 elements  
elements must be finate number

## buildRq
**name**:  
integer number in 0~9

number:
number

## stopOrder
no parameters

## holdPositionOrder
no parameters

## followOrder
**unitId**:  
integer number

**additive**:  
true or false

**orderId**:  
integer number

## selfDestructOrder
no parameters

## moveOrder
**points**:  
Array  
elements must be Array with 2 elements  
elements must be finate number

**additive**:  
true or false

**orderId**:  
integer number

## configGame
**config**:  
Object  
element 'type' must be in ["1v1", "1v1r", "1v1t", "2v2", "3v3", "survival"]

## startGame
no parameters

## addAi
**name**:  
string

**side**:  
string in ["alpha", "beta"]

**aiBuildBar**:  
Array with 10 elements  
element must be null or string

## switchSide
**side**:  
string in ["alpha", "beta", "spectators"]

## kickPlayer
**number**:  
integer number

## surrender
no parameters

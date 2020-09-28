# templatedcodegenerator
code generator with specified templates. replace and loops.

Functionalities:

loop.csv:

ModelName, PackageName

Player, main

Item, main

1.simple template replace.

DBMsgProcessorMap[protocol.DBMsgId_{{%=ModelName%}}Create] = MsgProcCreate{{%=ModelName%}}

will be replaced as

DBMsgProcessorMap[protocol.DBMsgId_PlayerCreate] = MsgProcCreatePlayer

2.loop support.

type DBUser struct {

    {{%loop.begin%}}
    
	model{{%=ModelName%}}s    map[string]*protocol.{{%=ModelName%}}
  
	modified{{%=ModelName%}}s map[string]*protocol.{{%=ModelName%}}

    {{%loop.end%}}
}

will be replaced as 

func NewDBUser() *DBUser {

	return &DBUser{
  
		modelPlayers:    make(map[string]*protocol.Player),
    
		modifiedPlayers: make(map[string]*protocol.Player),
    
		modelItems:    make(map[string]*protocol.Item),
    
		modifiedItems: make(map[string]*protocol.Item),
    
	}
  
}

3.loopIdx support.

package protocol

const DBMsgIdStart uint16 = 20000

{{%loop.begin%}}

const DBMsgId_{{%=ModelName%}}Create = DBMsgIdStart + {{%loop.lineIdx%}}

const DBMsgId_{{%=ModelName%}}CreateMany = DBMsgIdStart + {{%loop.lineIdx%}}

const DBMsgId_{{%=ModelName%}}Delete = DBMsgIdStart + {{%loop.lineIdx%}}

const DBMsgId_{{%=ModelName%}}DeleteMany = DBMsgIdStart + {{%loop.lineIdx%}}

const DBMsgId_{{%=ModelName%}}Update = DBMsgIdStart + {{%loop.lineIdx%}}

const DBMsgId_{{%=ModelName%}}UpdateMany = DBMsgIdStart + {{%loop.lineIdx%}}

const DBMsgId_{{%=ModelName%}}Select = DBMsgIdStart + {{%loop.lineIdx%}}

const DBMsgId_{{%=ModelName%}}SelectMany = DBMsgIdStart + {{%loop.lineIdx%}}

{{%loop.end%}}

will be replaced as 

package protocol

const DBMsgIdStart uint16 = 20000

const DBMsgId_PlayerCreate = DBMsgIdStart + 0

const DBMsgId_PlayerCreateMany = DBMsgIdStart + 1

const DBMsgId_PlayerDelete = DBMsgIdStart + 2

const DBMsgId_PlayerDeleteMany = DBMsgIdStart + 3

const DBMsgId_PlayerUpdate = DBMsgIdStart + 4

const DBMsgId_PlayerUpdateMany = DBMsgIdStart + 5

const DBMsgId_PlayerSelect = DBMsgIdStart + 6

const DBMsgId_PlayerSelectMany = DBMsgIdStart + 7


const DBMsgId_ItemCreate = DBMsgIdStart + 9

const DBMsgId_ItemCreateMany = DBMsgIdStart + 10

const DBMsgId_ItemDelete = DBMsgIdStart + 11

const DBMsgId_ItemDeleteMany = DBMsgIdStart + 12

const DBMsgId_ItemUpdate = DBMsgIdStart + 13

const DBMsgId_ItemUpdateMany = DBMsgIdStart + 14

const DBMsgId_ItemSelect = DBMsgIdStart + 15

const DBMsgId_ItemSelectMany = DBMsgIdStart + 16

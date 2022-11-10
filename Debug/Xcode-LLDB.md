# LLDB(Low-Level DeBugger) 란?
## LLVM(Low-Level Virtual Machine)
LLVM(Low-Level Virtual Machine)은 Apple에서 진행한 Compiler에 필요한 Toolchain 개발 프로젝트다.

LLDB는 LLVM의 Debugger Component를 개발하는 서브 프로젝트이며, LLVM 프로젝트를 통해 개발된 Clang Expression Parser, LLVM Diassembler 등 Low-Level 컨트롤이 가능한 모듈로 이루어져 있다. C, C++, Objective-C, Swift를 지원하며 현재 Xcode의 기본 Debugger로 내장되어있다.

# LLDB 명령어 기본 문법
`(lldb) command [subcommand] -option "argument"`

Command와 Subcommand는 LLDB 내 Object의 이름. (breakpoint, watchpoint, set, list ...) 이들은 모두 계층화 되어 있어, Command에 따라 사용 가능한 Subcommand 종류가 다르다.


## help
`(lldb) help`

LLDB에서 제공하는 Command를 출력해준다.

<br>

`(lldb) help <command>`

특정 Command의 SubCommand와 Option을 출력해준다.


## Apropos
`(lldb) apropos <keyword>`

특정 keyword의 상세한 설명을 출력해준다.

<br>

## po
### Object Description
`(lldb) expression -O -- <object>`

혹은

`(lldb) po <object>`

로 사용할 수 있고 object에 어떤 값이 저장되어 있는지, \<object\>에 대한 description이 출력된다.

혹은 런타임 때 변수값을 직접 수정할 수 있다.

`(lldb) expression -O -- <object> = <value>`

`(lldb) po <object> = <value>`

### 변수 생성
LLDB에서 런타임 때 직접 변수를 생성하고 사용할 수 있다.

`(lldb) po var(let) ${name} = {value}`

<br>

## breakpoint

### Line Breakpoint
![](https://user-images.githubusercontent.com/74440939/200708464-24b4fe12-631a-4f4b-805f-739b3c84923f.png)

Xcode IDE 왼쪽의 코드 라인을 클릭하면 breakpoint를 생성할 수 있다.

이렇게 코드의 라인에 생성한 breakpoint를 line breakpoint라고 한다.

<br>

### Column Breakpoint
![](https://user-images.githubusercontent.com/74440939/200710095-d494df4a-d459-4e19-bbb2-2611b077bb6a.png)

Xcode IDE에서 cmd를 누른 상태로 코드를 클릭해서 Create Column Breakpoint로 breakpoint를 생성할 수 있다.

이렇게 코드 라인 중 특정 부분에 생선한 breakpoint를 column breakpoint라고 한다.

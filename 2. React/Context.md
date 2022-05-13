# Context를 통한 전역 상태관리


## 도입 계기
1. useSocket이라는 훅을 만듦
    > socket.io 서버와 통신하여 데이터를 보내고 받는 기능을 함
2. 이 커스텀 훅을 여러 군데에서 사용해야 함
    > 각 클라이언트마다 하나의 socket으로 통신하고, 그 소켓을 통해 받는 데이터는 필요에 따라 여러 컴포넌트에서 공유해야 함
3. 그런데 해당 커스텀 훅을 각 컴포넌트마다 선언하니까 소켓이 여러개 생성됨


## 해결 과정
1. 먼저 useSocket 훅을 사용하는 컴포넌트에서는 고칠 것이 없음
    > 컴포넌트 부분에서는 작성할 때부터 단일 소켓을 여러 컴포넌트 사이에서 공유하는 것을 가정했기 때문에
2. createContext로 글로벌 컨텍스트를 생성함
3. provider를 만듦
    > 이 provider 안의 코드는 기존 useSocket의 코드를 거의 그대로 사용함. 단지 return 부분의 원래 반환하던 값을 Context.Provider 컴포넌트로 바꾼 다음 그것의 value로 기존 값을 넣어줌
4. 기존 코드가 빠져나간 useSocket은 이제 useContext(context)로 앞서 언급한 value를 받아서 그것을 그대로 반환함


## 효과
- 커스텀 훅을 단순히 만들어서 여러 군데에서 선언했을 때는 선언할 때마다 인스턴스가 만들어졌음
- useContext를 사용함으로써 소켓이 단일 인스턴스로 생성되었고 그것을 여러 컴포넌트에서 공유할 수 있게 됨


## 코드
    import { createContext, useContext, useEffect, useState } from 'react'
    import { io, Socket } from 'socket.io-client'
    import { Vector3 } from 'three'

    const PlayersContext = createContext<{socket:Socket, playerList:{ [key: string]: { pos: Vector3, action: string } }}>({socket:io(''), playerList:{}});
    const PlayersProvider = ({children}:{children:any}) => {
        const [socket, setSocket] = useState<Socket>(null!)
        const [socketConnected, setSocketConnected] = useState(false)
        const [playerList, setPlayerList] = useState<{ [key: string]: { pos: Vector3, action: string } }>({})
        useEffect(() => {
            setSocket(io(`localhost:2002`))
        }, [])

        useEffect(() => {
            if (!socket) return;
            socket.on('connect', () => {~~~});
            socket.on('disconnect', () => {~~~});
            socket.on('update', (data) => {
                setPlayerList(data)
            })
        }, [socket]);

        return <PlayersContext.Provider value={{ socket, playerList }} children={children} />
    }

    const useSocket=()=>{
        const {socket, playerList}=useContext(PlayersContext)
        return {socket, playerList}
    }

    export { PlayersProvider, useSocket }



Делаю опыты с gRPCна Windows  
Quick start здесь: https://grpc.io/docs/languages/go/quickstart/  
Скачивал protoc отсюда (раскрой кнопкой "треугольник" возле Assets):  
https://github.com/protocolbuffers/protobuf/releases?page=2  
Распаковал в папку C:\tmp  
Путь C:\tmp\protoc-24.2-win64\bin добавил в переменную среды Path  
Для редактирования переменной среды WIN + R, пишем sysdm.cpl  
Устанавливал плагины  
$ go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.28  
$ go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.2  
На гитхабе создал проект  
https://github.com/developerc/grpc2  
помогли команды  
git remote add origin https://github.com/developerc/grpc2.git  
git branch -M main  
git push -u origin main  
В VS создал модуль  
go mod init github.com/developerc/grpc2  
установим пакет grpc  
go get google.golang.org/grpc  
создал структуру папок проекта:  
.  
├── cmd    
│ ├── client // код запуска клиента  
│ └── server // код запуска сервера  
├── proto  
└── go.mod  
В каталоге proto создал файл geometry.proto  
В консоли Windows дал команду (в VS консоли не получается):  
C:\proj\Go\Sprint3\grpc2>protoc --go_out=. --go_opt=paths=source_relative     --go-grpc_out=. --go-grpc_opt=paths=source_relative     proto/geometry.proto  
в папке proto появились файлы geometry_grpc.pb.go и geometry.pb.go  
некоторые ссылки подчеркнуты красным, надо подтянуть зависимости:  
go mod tidy  
заполнили кодом ./cmd/server/main.go  
проверили как запускается сервер, потом остановим Ctrl+C  
go run ./cmd/server/main.go  
заполним кодом ./cmd/client/main.go  
запустим сервер в терминали VS  
go run ./cmd/server/main.go  
запустим клиент в Windows консоли  
go run ./cmd/client/main.go  
должны получить распечатку для клиента:  
Area:  207.05  
Perimeter:  61.2  
распечатка для сервера:  
1990/03/01 08:22:55 tcp listener started at port:  5000  
1990/03/01 08:23:17 invoked Area:  height:10.1 width:20.5  
1990/03/01 08:23:17 invoked Perimeter:  height:10.1 width:20.5  
  

- node不支持gbk，utf8一个汉字是三个字节
## buffer
- buffer一旦声明不能改变大小，而且创建时要指定大小
- 1）通过长度创建（字节数量创建）
- 2）通过数组创建buffer(如果是负 会加256，如果超出范围对256取模）
- 3）通过字符串创建
- buffer是按照字节长度来计算的，如果去buffer会自动转化成10进制
- 它拥有的方法有 forEach  slice
- buffer每一项的字节也是一个内存地址
- buffer.write
- buffer.copy
- Buffer.concat
## fs
- 操作文件fs模块file system是一个内置模块
- 方法是同步和异步同时出现，能用异步不会用同步
### readFile/readFileSync
- 可以读任意目录下的文件
- 1.读取的文件必须存在
- 2.默认读出的内容全部是buffer类型
- 3.会将全部内容读取到内存中，不能读取比内存大的文件
- 4.可以指定编码格式为utf8格式
- 同步方法处理异常可以用try catch
### writeFile/writeFileSync
- 1.默认写入编码格式是utf8
- 2.写入的内容会被toString
- 3.默认是清空 创建  仅写 w
### copy/copySync
    function copySync(source,target){
      let result=fs.readFileSync(source);
      fs.writeFileSync(target,result);
     }
     function copy(source,target,callback){
     fs.readFile(source,function(err,data){
     if(err)console.log(err);
     fs.writeFile(target,data,callback);
     })
     }
- 只能拷贝较小的文件，大文件会用流来处理
- 同步方法：现读取 再写入 ，如果读取的时候指定的是utf8那么读出来的是字符串否则就是buffer
### 创建目录
- fs.mkdirSync/fs.mkdir
## path
- path是node中一个核心模块，处理路径的
- 1.join 拼接 /resolve 解析
##　stream
- fs.createReadStream 创建可读流
- 特点
- 1.highWaterMark 高水位线，每次能读64k
- 2.读取的文件必须存在
- 3.默认读取到的内容是buffer
- let rs=fs.createReadStream('./name.txt',{highWaterMark:1});
- rs表示可读流对象
- 通过绑定事件可以触发数据的流动
- 默认叫非流动模式->流动模式
 let arr=[];
 rs.on('data',function(chunk){
 arr.push(chunk);
 rs.pause();//暂停data事件的触发，如果数据没有读完不会触发end事件
 });//监听数据到来的事件，可读流继承了事件，后台会不停的emit('data',读到的数据);
 setInterval(function(){
 rs.resume();//恢复触发data事件
 },1000);
//默认监听了on data事件会疯狂的读取，直到全部读完为止
 rs.on('end',function(){//监听数据读取完成，读取完成后会调用end事件
 })
### 创建可写流
- 1.没有则创建，内容全部清空，写入新内容
- 2.写入时编码格式是utf8
- 3.默认写入highWaterMark 16k
   let ws = fs.createWriteStream('./name.txt',{
   highWaterMark:1
   });
- 可写流有两个写数据的方法 write end
- 只接受 buffer 或者 字符串
  let flag=ws.write(1+'');//false
  我们可以控制写入，例如如果返回了false，不让它继续写了
- ws.end 只要调用end后会将write中的内容强制写到文件中
- on drain 当可写流内存全部写入后，会触发drain
### pipe 将可读流的内容，导入到可写流中
-- pipe 异步，读一点写一点 防止淹没可用内存 ，无法看到读到的内容
//读取默认64k 写入16k
  function pipe(source,target){
  let rs = fs.createReadStream(source,{
  highWaterMark:4
  });
  let ws = fs.createWriteStream({
  target,{highWaterMark:1
  });
  rs.on('data',function(data){
  let flag=ws.write(data);
  if(!flag)rs.pause();
  });
  ws.on('drain',function(){
  rs.resume();
  });
  rs.on('end',function(){
  ws.end();
  })
  }




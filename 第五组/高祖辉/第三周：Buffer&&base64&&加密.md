# 2017-5-6:Buffer&&base64&&加密
### 什么是Buffer？
	缓冲区Buffer是暂时存放在输入输出数据的一段内存。
	JS语言没有二进制数据类型，而在处理TCP和文件流的时候，必须要处理二进制数据
	NodeJS提供了一个Buffer对象来提供对二进制数据的操作
	Buffer是一个表示固定内存分配的全局对象，也就是说要放到缓存区中的字节数需要提前确定
	Buffer好比由一个多位字节元素组成的数组，可有效地在JavaScript中表示二进制数据
### 什么是字节？
	字节是计算机储存时的一种计量单位，一个字节等于8位二进制数
	一个位就代表一个0或1，每8个位（bit）组成一个字节（byte）
	字节是通过网络传输信息的单位
	一个字节最大值十进制数是255。在utf8中，一个汉字由三个字节组成。
### 定义Buffer的三种方式
>- 1、通过长度定义buffer。new Buffer(3);&ltBuffer 00 00 00>此时，buffer.length=3。buffer每一位是由两个16进制的数组成的（这表示buffer的一个字节长度），故而取值范围是[0,255]。
>- 2、	通过数组创建buffer（如果是负，会加256，如果超出范围会对256取模）。new Buffer([0x11,101,-1])。如果表达的是16进制直接使用，其他的十进制需要转化成16进制。
>- 3、通过字符串创建 。new buffer('主峰')，此时buffer.length=6.如果想获得buffer[index]的值得到是na一位buffer转化成十进制的值值会导致源buffer的改变，类似于数组中放入一个一个数组，此时在里面的数组存放的就是地址
>- Buffer的每一项的字节就是一个内存地址，改变某一项的buffer 
### Buffer常用的方法
	1、fill方法
	buffer.fill(0);手动初始化，将buffer内容清零
	2、write方法
	buffer.write(string,offset,length,encoding)
	stringn 写入的字符串
	offset 在buffer中的偏移量
	length 写入的字符串的长度，可以不写，默认全长，多余的舍掉
	3、toString方法
	buffer.toString('utf8',start,end)
	将buffer转化成字符串start，end是截取的buffer的长度
	4、slice方法
	有截取乱码的问题
	5、copy方法
	sourceBuffer.copy(targetBuffer,targetStart,sourceStart，sourceEnd)
	sourceBuffer 被复制的文件
	targetBuffer 将要得到的文件
	targetStart 在得到的文件中的起始位置，包前不包后，后面可以被覆盖掉。
	sourceStart，sourceEnd 复制的位置
	5、Buffer.concat 方法，属于Buffer上的方法
	Buffer.concat([buffer1,buffer2,buffer3])拼接完成后返回一个大buffer	
	6.Buffer.byteLength('string')
	获得string的字节长度
```
//1.写长度过长，截取有效长度
//2.过短 多的就被截取掉
//3.不传递长度，默认全部拼接 myConcat
function myConcat(list,totalLength){
	if(typeof totalLength =='undefined'){
		totalLength=list.reduce(function(prev,next){
			return prev.length+next.length;
		},0))
	}
}
let buffer=new Buffer(totalLength);
let index=0;
list.forEach(item=>{
item.copy(buffer,index);
index+=item.length;
})
return buffer.slice(0,index);
```
### 进制的转化
>- parseInt('数字'，进制数) 任意进制转化为10进制
>- (数字).toString(进制数) 10进制转化成任意进制，如果数字放的是0x开头则代表的是16进制，如果数字以0开头则表示八进制	
### 加密
> 1、crypto
	
	crypto是node.js中实现加密和解密的模块 在node.js中，使用OpenSSL类库作为内部实现加密解密的手段 OpenSSL是一个经过严格测试的可靠的加密与解密算法的实现工具。
> 2、散列（哈希）算法
	
	散列算法也叫哈希算法，用来把任意长度的输入变换成固定长度的输出,常见的有md5,sha1等，特点如下：
	1、相同的输入会产生相同的输出
	2、不同的输出会产生不同的输出
	3、任意的输入长度输出长度是相同的
	4、不能从输出推算出输入的值，不可逆。
	获取所有的散列算法：crypto.getHashes()
	散列算法示列：
	var crypto = require('crypto');
	var md5 = crypto.createHash('md5');//返回哈希算法
	var md5Sum = md5.update('hello');//指定要摘要的原始内容,可以在摘要被输出之前使用多次update方法来添加摘要内容
	var result = md5Sum.digest('hex');//摘要输出，在使用digest方法之后不能再向hash对象追加摘要内容。
	console.log(result);
>- 3、HMAC算法
		
	md5算法容易被彩虹表攻击,彩虹表就是描述()明文->密文)对应关系的一个大型数据库，破解时通过密文直接反查明文。
	HMAC算法将散列算法与一个密钥结合在一起，以阻止对签名完整性的破坏 生成私钥
	$ openssl genrsa -out key.pem 1024
	var crypto = require('crypto');
	var shasum = crypto.createHmac('sha1', 'zfpx');
	var result = shasum.update('hello').digest('hex');
	console.log(result);
### base64
	base64不是加密算法，可逆。
	base64中一个汉字是3个字节，24位，将24位拆分成4段。
	一个汉字3个字节都是16进制
	通过().toString(2)将16进制转化成2进制
	此时一个字节的最大值是255，而base64中的每个字节转化成10进制都不会大于64，所以每段取六位，每六位的二进制编码在转化成10进制，在可见编码中取值即可，此时范围是[0,63];
	parseInt('6位二进制数'，2)
	'26个大写字母，小写字母,0123456789,+/'从这其中取值，就是base64编码



	
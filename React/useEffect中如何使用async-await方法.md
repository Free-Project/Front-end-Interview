# useEffect中如何使用 async/await
如果在useEffct中直接使用async/await方法就会出现警告：
> Warning: useEffect function must return a cleanup function or nothing. Promises and useEffect(async () => …) are not supported, but you can call an async function inside an effect..
代码如下
```
const [data, setData] = useState({});
useEffect(async () => {
  await axios(url).then((result) => setData(result.data));
}, []);
```
原因是async函数默认会返回一个Promise对象，而useEffect中，只允许什么都不返回或者返回一个清除函数。

推荐写法：
```
const [data, setData] = useState({});
useEffect(() => {
  const fetchData = async () => {
    const result = await axios(url);
    setData(result.data);
  };
  fetchData();
}, [])
```

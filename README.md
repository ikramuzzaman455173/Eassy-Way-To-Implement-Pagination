<h1 align="center">Eassy Way To Implements React Paginations</h1>

### Pagination Server Side Code:)

```javascript

app.get('/allToys',async (req, res) => {
      const { sort } = req.query;
      let sortQuery = {};
      if (sort === 'asc') {
        sortQuery = { price: 1 };
      } else if (sort === 'desc') {
        sortQuery = { price: -1 };
      }
      const limit = parseInt(req.query.limit) || 10
      const page = parseInt(req.query.page) || 1
      const skip = (page - 1) * limit

      const result = await toysRusCollection.find({}).sort(sortQuery).limit(limit).skip(skip).toArray();
        res.send(result)
    });
 ```
    
### Pagination Client Side Code:)
    
 ```jsx
    const [page, setPage] = useState(1)
  const [limit, setLimit] = useState(5)
  const [totalItems, setTotalItems] = useState(0)
  useEffect(() => {
    fetch(`http://localhost:4000/totalToys`)
      .then(response => response.json())
      .then(data => {
        console.log(data)
        setTotalItems(data.count)
      }).catch(error => console.log(`404 page not found ${error}`))
  }, [])

  fetch(`http://localhost:4000/allToys?sort=${sortingOrder}&limit=${limit}&page=${page}`)
```
  
  ### DasiUI Pagination Button :)
  
  ```jsx
    <div className="flex justify-between items-center">
        <div className="join text-center mx-20 my-20">
          <button className="join-item btn" onClick={() => {
            page === 1 ? setPage(1) : setPage(page - 1)
          }} disabled={page === 1}>«</button>
          <button className="join-item btn">Page {page}</button>
          <button className="join-item btn" onClick={() => {
            page === Math.round(totalItems / limit) ? setPage(Math.round(totalItems / limit)) : setPage(page + 1)
          }} disabled={page === Math.round(totalItems / limit)}>»</button>
        </div>
```            

```jsx
        <select className="select select-success w-full max-w-xs mx-20" value={limit} onChange={e => setLimit(e.target.value)}>
          <option disabled>Select Show The View 1 Page Total Items?</option>
          <option value={5}>5</option>
          <option value={10}>10</option>
          <option value={15}>15</option>
          <option value={20}>20</option>
        </select>
      </div>
 ```
      
 ### Pagination Table Index Controls:)
      
 ```jsx
      {(page - 1) * limit + index + 1}
```

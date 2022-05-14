# Cheat Sheet personnel pour une application MEAN Stack


Récupérer les données de la BDD MongoDB :
````
// app.js
app.get('/api/films', function(req, res){
    db.collection('movies').find({ type : "Film"}).sort({ nbVotes: -1 }).toArray(function(err, users){
        if (err) throw err;
        res.json(users)
    })
})

````
# Récupérer les données de l'api :
````
// app.component.ts
export class AppComponent {
  url = 'http://localhost:3001/api/films';
  movies = [];
 
constructor(private http: HttpClient){
  this.http.get(this.url).toPromise().then((data: any) => {
    this.movies = data
 
   
  })
}
````

# Récupérer data selon l'_id dans MongoDB :
````
// app.js
db.collection('users').findOne({ _id: ObjectId(`${req.params.id}`)}
````

# Déclarer une session dans un component :
````
// ***.component.ts
sessionStorage.setItem('name', 'Antoine');
````


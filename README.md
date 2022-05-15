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

# Passer la valeur d'un input vers nodeJS :
````
<input type="text" name="nom" placeholder="Nom de famille" [(ngModel)]="input.nom">
````
````
  input: any = {
    prenom: "",
    nom: "",
    email: "",
    password: "",
};

register(){
    this.http.post('http://localhost:3001/register', this.input)
        .subscribe(
          (            next: any) => {
                // TO-DO Success event
                console.log('success')
            },
          (            error: any) => {
                // TO-DO Error event
                console.log('error')
            });
}
````

````

app.post('/register', function(req, res){
    db.collection('users').insertOne({
        prenom : req.body.prenom,
        nom: req.body.nom,
        email : req.body.email,
        password : req.body.password
    })
})

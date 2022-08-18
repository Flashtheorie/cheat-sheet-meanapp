### Cheat Sheet personnel pour une application MEAN Stack

# Table des matières :
[Récupérer les données de la BDD MongoDB](#fetchdatabdd)
[Récupérer les données de l'api](#fetchdataapi)
# <a name="fetchdatabdd">Récupérer les données de la BDD MongoDB</a> :
````
// app.js
app.get('/api/films', function(req, res){
    db.collection('movies').find({ type : "Film"}).sort({ nbVotes: -1 }).toArray(function(err, users){
        if (err) throw err;
        res.json(users)
    })
})

````
# <a name="fetchdataapi">Récupérer les données de l'api :</a>
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

````


# Récupérer l'_id de l'user qui vient d'être crée :
````
app.post('/register', function(req, res){
     db.collection('users').insertOne({
        prenom : req.body.prenom,
        nom: req.body.nom,
        email : req.body.email,
        password : req.body.password,
        solde : 0,
        economies : 0
    }, function(err, user){
        res.json(user.insertedId)
    })

})

````


````
register(){
    this.http.post('http://localhost:3001/register', this.input)
        .subscribe(result => {
          console.log(result);
        })
}


````
# Full registerComponent :

````

import { Component, OnInit } from '@angular/core';
import { HttpClient } from '@angular/common/http';
@Component({
  selector: 'app-register',
  templateUrl: './register.component.html',
  styleUrls: ['./register.component.css']
})
export class RegisterComponent {
  input: any = {
    prenom: "",
    email: "",
    password: "",
};
data: any;
error: boolean | undefined;
errorMessage: string | undefined;

  register(){
    this.http.post('http://localhost:3001/register', this.input)
        .subscribe(result => {
          const removeQuotes = JSON.stringify(result)
          const removed = removeQuotes.replaceAll('"', '');
          sessionStorage.setItem('id', removed)
        })
}


constructor(public http: HttpClient){
    
}

}
````

# Display a rank and update the rank :

````
db.collection('websites').find({}).sort({  "points": -1 }).forEach(doc => {

  rank++;
  doc.rank = rank;
  //delete doc._id;
  //console.log(doc._id);

  db.collection('websites').updateOne({_id : doc._id},
    { $set: { rank: doc.rank } },
    { upsert: true }
)

})
````



# Get data from URL :

````
routes : 
{ path: 'product/:id', component: ProductComponent, canActivate: [AuthGuard]},

.ts : 
import { Component, OnInit } from '@angular/core';
import {ActivatedRoute} from '@angular/router';
@Component({
  selector: 'app-product',
  templateUrl: './product.component.html',
  styleUrls: ['./product.component.css']
})
export class ProductComponent implements OnInit {

  constructor(private route: ActivatedRoute) {
    console.log(this.route.snapshot.params["id"]) // <------ this
  }

  ngOnInit(): void {
  }

}
````

# Additionner des datas
````

app.get('/api/gains/totaux', function(req, res){
    db.collection('gains').aggregate([
        {
            $group: {
              _id: null,
              total: {
                $sum: "$amount"
              }
            }
          }
      ]).toArray(function(err, result){
            
            if(err){
                res.send(err)
            }
            else{
                res.json(result)
                
            }
        }
    )}
);
````

# Modifier toutes les données d'un coup
````
db.users.updateMany({}, { $set: { premium: 0 } })
````

#  This condition will always return True/False
````
*ngIf="!(photosliked | keyvalue)?.length"
````

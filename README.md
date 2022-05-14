# cheat-sheet-meanapp
Cheat Sheet personnel pour une application MEAN Stack


# Récupérer les données de l'api :
````
export class AppComponent {
  url = 'http://localhost:3001/api/films';
  movies = [];
 
constructor(private http: HttpClient){
  this.http.get(this.url).toPromise().then((data: any) => {
    this.movies = data
 
   
  })
}


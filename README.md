# GY4

saját folyamatok kilistázása: `ps aux | sajátazonosító`
>  2^4 foylamatunk van
>  a prompt hamarabb ér vissza mert a szülő folyamat befejeződik, de a gyerek nem, ezt `wait` vagy `waitpid` -del kivédhető, a `wait` tel egy tetszőleges foylamatra várok, míg utóbbival megmondható hogy pontosan melyikre.

```` C
int main (){

//printf("%i/n",getpid());
//pid_t child=fork (); //froks make a copy of variables
int x = 5;
pid_t parent = getpid();
pid_t child=fork();
if (parent == getpid()){
    x = 6;
    int status;
    wait(&status);
} else {
    x=7;
}
printf("%i \n",x);

//int i;
//for (i=0; i<4;i++)
//    fork();

// printff("%i %i \n", getpid(), getppid());
return 0;
}
````

### Output
````C
6        //amikor létrejön a folyamat kap egy területet oda bemásolódik az összes változó és a nevük hiába ugyanaz, más értéket hordoznak
7
````
> ezért


```` C
int main (){
    int x = 5;
    //pid_t parent = getpid();
    pid_t child=fork(); //forks me a copy of variables
    // if (child>0){  perror();  .... }  //ha nem jön létre gyerek folyamat
                         //perror ír ki a standard error csatornára
    if (child>0){
        x = 6;
        int status;
        wait(&status);
    } else {
        x=7;
    }
    printf("%i \n",x);
    return 0;
}
````

> ha nincs szülője egy folyamatnak akkor az egyees sorszámú lesz az
> program indítás `./fájlnév`

### Külső program indítása
> `execv(parancs, argumentum amit a program várna)`
> az atrgumentum az egy `arg[] = {elso, masodik, .. NULL};` formában kell megadni, azaz, a `NULL` feltétlen szükséges, mert az zárja le a promptot
karaktertömb gész típusra `atoi` -vel

`system("./write 'Operating Systems' 5");`

> miért `exec`?
Mert a `system`egy `execet`használ

# Algorithmique et programmation avancée 
## Série de TP 1 : Pr:AMAMOU Ahmed
### Objectif : Manipulation des structures

Dans une unité d'assemblage des ordinateurs, les composants électroniques utilisés peuvent être réalisés par plusieurs fabricants. Selon le mode de communication, les composants sont regroupés par classes (PCI, ISA,...). Pour une meilleure organisation, la direction opte de représenter les informations techniques de ces composants par un tableau de structures et de les gérer par un programme C. on suppose qu'un composant est caractérisé par un Code, un Nom, une Classe, un Fabricant, une date de fabrication (Date fab).

##  Définir les structures date et composant.

```c
//définir les structures date et composants 
typedef struct {
int jour ;
int mois;
int annee;
}DATE;

typedef struct {
    int code;
    char nom[40];
    char classe[40];
    char fabricant[40];
    DATE datefab;
}COMPOSANTS;
```

## Ecrire une fonction qui saisit une date.
```c
//saisir la date
void saisirDate(DATE *X)
{
    printf("donnez le jour : \n");
    scanf("%d",&X->jour);
     printf("donnez le mois : \n");
    scanf("%d",&X->mois);
     printf("donnez l'annee : \n");
    scanf("%d",&X->annee);
};
```

##  Ecrire une fonction qui affiche une date.
```c
//afficher la date
void afficherDate (DATE X)
{
    printf("la DATE est %d / %d / %d",X.jour,X.mois,X.annee);
} 
```
## Ecrire une fonction qui saisit un composant.
```c
//fonction qui saisit un composant 
void saisirComposant (COMPOSANTS * c){
    printf("donnez le code : \n");
    scanf("%d",&c->code);
    printf("donnez le nom : \n");
    scanf("%s",&c->nom);
    printf("donnez la classe : \n");
    scanf("%s",&c->classe);
    printf("donnez le fabricant : \n");
    scanf("%s",&c->fabricant);
    //scanf("%d",&c->datefab.jour);
    saisirDate(&c->datefab);

}
```
## Ecrire une fonction qui affiche un composant.
```c
//afficher un composant
void afficheComposants (COMPOSANTS c){
    printf("\nle code est : %d\n le nom est: %s \nla classe est %s\nle fabricant est %s\n",c.code,c.nom,c.classe,c.fabricant);
  
    afficherDate(c.datefab);   
}
```
## Ecrire une fonction qui saisit un tableau de composants.
```c
//fonction qui saisit un tableau de COMPOSANTS
void tableauComposants(COMPOSANTS *c, int taille ){
    int i;
    for(i=0;i<taille;i++){
        saisirComposant(&c[i]);
    }
}
```
## Ecrire une fonction qui affiche un tableau de composants.
```c
//afficher un tableau de COMPOSANTS 

void afficherTableau(COMPOSANTS *c ,int taille){
   	int i;
   	for(i=0;i<taille;i++){
   		afficheComposants (c[i]);
	   }
}
```
## Ecrire le programme principal qui réalise le scénario suivant :
 -  Déclaration d'un tableau dynamique de composantes.
  - Saisie d'un tableau de composants. 
  -  Affichage d'un tableau de composants.
```c
int main (){

DATE d;
COMPOSANTS c;
int taille =2;

//déclaration d'un tableau dynamique de composants 
COMPOSANTS *t =malloc(taille*sizeof(COMPOSANTS));

//saisie du tableau de composant
tableauComposants(&c,taille);

//affichage du tableau de composants
afficherTableau(&c,taille);
```
## Ecrire une fonction qui calcule le nombre de composants réalisés par un fabricant donne.
```c
//fonction qui calcule le nombre de COMPOSANTS réalisé par un fabricant
   
int nbrFabricant(COMPOSANTS *c ,char fabricant[],int taille){
int n=0;	
int i=0;
for(i=0;i<taille;i++){
//strcmp est une fonction qui revoie 0 si les chaines de caractère sont les memes 
 if(strcmp(fabricant,c[i].fabricant)==0){
	n++;
	}
}
return n;	
}

```
## Ecrire une fonction qui calcule le nombre de composants de deux classes données (exemple "PCI" ou "ISA").
```c
//fonction qui calcule le nombre de COMPOSANTS de deux classes données

int nbrComposant (COMPOSANTS *c,char classe1[],char classe2[],int taille){
	 
int n=0;
int i;
for(i=0;i<taille;i++){
	if(strcmp(classe1,c[i].classe)==0||strcmp(classe2,c[i].classe)==0){
		n++;
	}
}
return n;	
}
```
## Ecrire une fonction qui affiche les composants fabriqués entre deux dates d1 et d2.
```c
int composantsEntreDates (COMPOSANTS*c,DATE d1,DATE d2,int taille){
int n=0;
int i;
//pour comparer les dates on passe d'abord par comparer les années passant par les mois puis les jours 
for(i=0;i<taille;i++){
  if(c[i].datefab.annee>=d1.annee&&c[i].datefab.annee<=d2.annee){
	if(c[i].datefab.mois>=d1.mois&&c[i].datefab.mois<=d2.mois){
	        if(c[i].datefab.jour>=d1.jour&&c[i].datefab.jour<=d2.jour){
	               n++;
		}
	}
   }
}
return n;
}
```
## Ajouter au programme principal précédent les fonctionnalités suivantes :

- Calcul du nombre de composants réalisés par un fabricant donne. 
-  Calcul du nombre de composants de deux classes données (exemple "PCI ou "ISA"). 
-  Affichage des composants fabriqués entre deux dates d1 et d2
```c

	
int main (){

DATE d;
COMPOSANTS c;
int taille =2;

DATE d2={10,3,2002};
DATE d1={2,12,2002};

//calcul de composant réalisé par un fabricant
printf("\n le nbr de composants realises par firdawse est %d \n",nbrFabricant(&c ,"firdawse",taille));

//nbr de composants de deux classes
printf("le nbr de composants des deux classe pci et isa est %d  \n",nbrComposant (&c,"pci","isa",taille));

//affichage de composants fabriqués entre deux dates
printf("le nbr de composants entre d1 et d2 est %d ",composantsEntreDates (&c,d1,d2,taille));

}  
```

# Merci !

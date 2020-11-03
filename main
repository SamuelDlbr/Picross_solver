# -*- coding: utf-8 -*-
"""
Created on Fri Dec 22 19:23:59 2017
Finished on Sun Dec 24 13:05:07 2017
@author: Samuel
"""
import matplotlib.pyplot as plt
def afficher2 (ListeBlocs,ListeTrous):
    Ligne=[]
    for j in range(ListeTrous[0]):
            Ligne.append(0)
    for j in range(ListeBlocs[0]):
        Ligne.append(1)
    for i in range(1,len(ListeBlocs)):
        for j in range(ListeTrous[i]+1):
            Ligne.append(0)
        for j in range(ListeBlocs[i]):
            Ligne.append(1)
    for j in range(ListeTrous[-1]):
            Ligne.append(0)
    return(Ligne)

def partition(n,k):
    if n==0:
        return([[0 for i in range(k)]])
    elif n==1:
        L=[]
        for i in range(k):
            elt=[0 for j in range(k)]
            elt[i]+=1
            L.append(elt)
        return(L)
    else :
        L=partition(n-1,k)
        Lp=[]
        for i in range(len(L)):
            for j in range(k):
                elt=L[i][:]
                elt[j]+=1
                Lp.append(elt)
        
        for i in range(len(Lp)):
            for j in range(len(Lp)):
                if j!=i and Lp[i]==Lp[j]:
                    Lp[i]=7
        i=0
        while i< len(Lp):
            if Lp[i]==7:
                del Lp[i]
            else :
                i+=1
        return(Lp)

def genermat(taille,Blocs):
    A=[]
    n=taille-sum(Blocs)-len(Blocs)+1
    k=1+len(Blocs)
    ListeTrous=partition(n,k)
    for i in range(len(ListeTrous)):
        A.append(afficher2 (Blocs,ListeTrous[i]))
    return(A)

def simpl(A,line):
    i=0
    while i< len(A):
        convient=1
        for j in range(len(A[i])):
            if A[i][j]==1 and line[j]==0 or A[i][j]==0 and line[j]==1:
                convient=0
        if convient==0:
            del A[i]
        else :
            i+=1
    return A

def applyline(blocs,line):
    taille=len(line)
    A=genermat(taille,blocs)
    A=simpl(A,line)
    Res=mash(A)
    return(Res)

def mash(A):
    Res=[2 for i in range(len(A[0]))]
    for i in range(len(A[0])):
        que1=1
        que0=1
        for j in range(len(A)):
            if A[j][i]!=1:
                que1=0
            if A[j][i]!=0:
                que0=0
        if que1==1:
            Res[i]=1
        if que0==1:
            Res[i]=0
    return(Res)

def passage(Grid,L):
    for i in range(len(L)):
        blocs=L[i][:]
        line=Grid[i][:]
        Res=applyline(blocs,line)
        Grid[i]=Res[:]
    return(Grid)

def Max(a,b):
    if a>b:
        return(a)
    else :
        return(b)

def transpose(Grid):
    m=Max(len(Grid[0]),len(Grid))
    Res=[[2 for i in range(m)] for j in range(m)]
    for i in range(m):
        for j in range(m):
            Res[j][i]=Grid[i][j]
    return(Res)

def solve(L1,L2):
    m=Max(len(L1),len(L2))
    Grid=[[2 for i in range(m)] for j in range(m)]
    solved=0
    while solved==0:
        Grid=passage(Grid,L1)
        Grid=transpose(Grid)
        passage(Grid,L2)
        Grid=transpose(Grid)
        solved=1
        for i in range(len(Grid[0])):
            for j in range(len(Grid)):
                if Grid[i][j]==2:
                    solved=0       
    Grid=transpose(Grid)
    X=[]
    Y=[]
    for i in range(len(Grid)):
        for j in range(len(Grid[i])):
            if Grid[i][j]==1:
                X.append(len(Grid)-i)
                Y.append(j)
    plt.scatter(Y,X,s=200,marker='s')

        
if __name__ == '__main__':

#   L1=[[2,1],[4,1],[2,4,1],[8],[7],[6],[1,7],[1,5],[3],[1,1]]
#   L2=[[2],[2,2],[2,1],[6],[9],[9],[8],[7],[1,3],[2,1]]

   L1=[[4],[4],[8],[6,2],[10],[6,2],[6,1],[8,1],[7],[3],[2]]
   L2=[[3],[3],[5],[5,1],[7],[9],[9],[8],[6],[3],[1,1],[6],[3]]
   solve(L1,L2)

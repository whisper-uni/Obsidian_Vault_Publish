 L’obiettivo della cluster analysis è quello di minimizzare la varianza ($Var_w$) all’interno del cluster (Within cluster variance), e di massimizzare la varianza ($Var_b$) tra i cluster (Between cluster variance).  In termini matematici si ottiene:

$Var_w(X)=E[(X-µ)^2]$                   $Var_b(Y)=E[(Y-µ)^2]$

$W_k=Var_w/Var_b$


Si sta dunque cercando di accorpare quanto più possibile la presenza di punti intorno ad un centroide che rappresenta un cluster, mantenendo il più possibile separati questi punti da quelli appartenenti ad altri cluster. Quello che si fa per scegliere k è di adottare il cosiddetto "Criterio del Gomito": all’aumentare del numero k di cluster ovviamente il rapporto $W_k$ diminuisce. Ad un certo punto il guadagno marginale che si ottiene aggiungendo un nuovo cluster diminuirà drasticamente, generando un angolo nel grafico che rappresenta il rapporto $W_k$ e il numero di cluster. Graficamente la situazione è quella mostrata sotto:

![[Pasted image 20250529222504.png]]


Dunque all’aumentare del numero di cluster k il rapporto tra le varianze Wk diminuisce, quindi il guadagno che si ottiene aggiungendo un nuovo cluster diminuisce nel tempo fino a divenire trascurabile. Quindi si può scegliere il numero di cluster k che meglio rappresentano in modo congruo ed omogeneo l’insieme di dati che si ha a disposizione.
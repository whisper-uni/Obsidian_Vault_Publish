Il Mean Variance Scaling, o Standardizzazione dei dati, è una tecnica di normalizzazione delle feature che consiste nel trasformare le feature in modo che abbiano una media zero e una deviazione standard unitaria. In pratica, per ogni feature, si sottrae la media dei suoi valori e poi si divide per la deviazione standard. Questo processo fa sì che le feature abbiano una distribuzione con media zero e varianza unitaria, rendendo più facile per i modelli di machine learning confrontare e interpretare i dati. Questa tipologia di trasformazione non conserva la sparsità dei dati: i valori che in precedenza erano nulli ora sono modificati. Inoltre, poiché sia la media che la varianza dipendono da tutti i campioni e non solo dal più grande o dal più piccolo, questo metodo, a differenza dei precedenti, non è influenzato dagli outlier.

i valori della distribuzione normale sono tabulati per media zero e varianza unitaria.

Il procedimento prevede di sottrarre alla variabile aleatoria la sua media e dividere il tutto per la [[deviazione standard ]] (cioè la radice quadrata della [[Varianza]]):

    ${\displaystyle Z={\frac {X-\mu }{\sigma }}.}$
    


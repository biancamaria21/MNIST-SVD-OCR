# MNIST-SVD-OCR

## Descriere

Proiectul recunoaște cifrele scrise de mână (0-9) din setul de date MNIST. Fiecare imagine are 28×28 pixeli, adică un vector de 784 de valori. Comparând direct cei 784 de pixeli, două imagini diferite ale aceleiași cifre pot părea foarte diferite. Pentru a rezolva această problemă, proiectul extrage geometria cifrelor cu ajutorul **Descompunerii Valorilor Singulare (SVD)**, reducând comparația de la 784 de dimensiuni la 30.

## Metoda

1. **SVD manual:** matricea de imagini este descompusă folosind valorile și vectorii proprii ai lui $A^T A$ (`numpy.linalg.eigh`). Coloanele din $U$ sunt cunoscute ca „eigen-digits”.
2. **Proiecție:** se păstrează primele $k = 30$ componente din $U$, iar imaginile de antrenament sunt proiectate în acest subspațiu redus.
3. **Clasificare:** pentru o imagine nouă, se proiectează și se alege eticheta celei mai apropiate imagini de antrenament, măsurată cu norma 2 (clasificator Nearest Neighbor în spațiul redus).

## Rezultate

Experimentele sunt făcute cu 10 000 de imagini de antrenament și 2 000 de imagini de test.

| k  | Acuratețe |
|----|-----------|
| 5  | 66,7%     |
| 10 | 88,9%     |
| 20 | 94,5%     |
| 30 | 96,0%     |
| 40 | 95,8%     |

Acuratețea crește odată cu $k$, dar timpul de testare crește și el. Peste un anumit punct, componentele suplimentare nu mai aduc câștig semnificativ.

Proiectul compară și implementarea manuală a SVD-ului cu `numpy.linalg.svd`. Ambele dau aceleași valori singulare, cu o diferență relativă de ordinul $10^{-8}$.

## Structura

- `PROIECT_MN (1).ipynb`: notebook-ul principal, cu explicații, implementare, benchmark, evaluare și concluzii.

## Cerințe

- Python 3.9+
- numpy, matplotlib, scikit-learn, pandas, pillow

```bash
pip install numpy matplotlib scikit-learn pandas pillow
```

## Rulare

1. Deschide notebook-ul în Jupyter sau în Google Colab.
2. Rulează toate celulele în ordine (**Runtime → Run all** în Colab).
3. Descărcarea MNIST se face automat la prima rulare și necesită conexiune la internet.

În Google Colab, a doua parte a notebook-ului include un canvas în care poți desena o cifră și primești predicția. Local, această secțiune afișează doar un mesaj.

I, [core] Kha?i nie??m tight-coupling (lie?n ke??t ra?ng buo??c) va? ca?ch loosely coupled
1, Gi?i thi?u
- tight-coupling (li�n k?t r?ng bu?c) l� m?t kh�i ni?m trong java �m ch? vi?c m?i quan h? gi?a c�c class qu� ch?t ch?. Khi y�u c?u thay ??i logic hay m?t class b? l?i d?n t?i ?nh h??ng t?i to�n b? c�c class li�n quan ??n n�.
- Loosely-coupled l� c�ch �m ch? vi?c l�m gi?m b?t s? ph? thu?c gi?a c�c class v?i nhau.
VD: 
	1, B?n c� m?t Class th?c thi m?t nhi?m v? c?c k? ph?c t?p, v� m?t trong s? ?� l� vi?c s?p x?p d? li?u tr??c khi x? l�.

public class BubbleSortAlgorithm{

public void sort(int[] array) {
// TODO: Add your logic here
    System.out.println("?� s?p x?p b?ng thu?t to�n sx n?i b?t");
  }
}



public class VeryComplexService {
// t?o m?i 1 th?ng BubblesortAlgorithm
private BubbleSortAlgorithm bubbleSortAlgorithm = new BubbleSortAlgorithm();
public VeryComplexService(){
}

public void complexBusiness(int array[]){
   bubbleSortAlgorithm.sort(array);
// TODO: logic here
  }
}

- V?i c�ch l�m ? tr�n, VeryComplexService ?� ho�n thi?n ???c nhi?m v?, tuy nhi�n, khi c� y�u c?u thay ??i thu?t to�n s?p x?p sang QuickSort th� nghe v? ch�ng ta s? ph?i s?a l?i ho�n to�n 2 Class ? tr�n ( s?a logic ? BubbleSortAlgorithm v� s?a l?i bi?n ? VeryComplexService )
- Ngo�i ra BubbleSortAlgorithm s? ch? t?n t?i n?u VeryComplexService t?n t?i, v� VeryComplexService t?o ??i t??ng BubbleSortAlgorithm b�n trong n� ( hay n�i c�ch kh�c l� s? s?ng ch?t c?a BubbleSortAlgorithm s? do VeryComplexService quy?t ??nh ), theo nh? c�ch impplement n�y, n� l� li�n k?t r?t ch?t v?i nhau
	2,  

public interface SortAlgorithm {
    /**
     * S?p x?p m?ng ??u v�o
     * @param array
     */
    public void sort(int array[]);
}

public class BubbleSortAlgorithm implements SortAlgorithm{

    @Override
    public void sort(int[] array) {
        // TODO: Add your logic here
        System.out.println("?� s?p x?p b?ng thu?t to�n sx n?i b?t");
    }
}

public class VeryComplexService {
    private SortAlgorithm sortAlgorithm;
    public VeryComplexService(){
        sortAlgorithm = new BubbleSortAlgorithm();
    }

    public void complexBusiness(int array[]){
        sortAlgorithm.sort(array);
        // TODO: more logic here
    }
- V?i c�ch l�m n�y, VeryComplexService s? ch? quan h? v?i m?t interface l� SortAlgorithm v?i c�ch n�y th� m?i quan h? gi?m b?t s? li�n k?t, nh?ng n� kh�ng thay ??i ???c vi?c thu?t to�n v?n ?ang l� BubbleSortAlgorithm
	3, c�ch 3
public interface SortAlgorithm {
     * S?p x?p m?ng ??u v�o
    public void sort(int array[]);
}

public class BubbleSortAlgorithm implements SortAlgorithm{
    @Override
    public void sort(int[] array) {
        // TODO: Add your logic here
        System.out.println("?� s?p x?p b?ng thu?t to�n sx n?i b?t");
}}

public class QuicksortAlgorithm implements SortAlgorithm {
    @Override
    public void sort(int[] array) {
        // TODO: Add your logic here
        System.out.println("?� s?p x?p b?ng thu?t sx nhanh");
}}

public class VeryComplexService {
    private SortAlgorithm sortAlgorithm;
    public VeryComplexService(SortAlgorithm sortAlgorithm){
        this.sortAlgorithm = sortAlgorithm;
    }

    public void complexBusiness(int array[]){
        sortAlgorithm.sort(array);
        // TODO: more logic here
    }
}
public static void main(String[] args) {
    SortAlgorithm bubbleSortAlgorithm = new BubbleSortAlgorithm();
    SortAlgorithm quickSortAlgorithm = new QuicksortAlgorithm();
    VeryComplexService business1 = new VeryComplexService(bubbleSortAlgorithm);
    VeryComplexService business2 = new VeryComplexService(quickSortAlgorithm);
}
- C�ch th? ba n�y c?ng l� c�ch ph? bi?n nh?t. M?i li�n h? gi?a 2 Class ?� �l?ng l?o� h?n tr??c r? nhi?u. VeryComplexService s? kh�ng quan t�m ??n thu?t to�n s?p x?p l� g� n?a, m� ch? c?n t?p trung v�o nghi?p v?. C�n SortAlgorithm s? ???c ??a v�o t? b�n ngo�i t�y theo nhu c?u s? d?ng.




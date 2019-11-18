# Breath-sourch-algoritm-maze-en-k-sa-yol
class dugum {
	// (x, y) matris hücre koordinatlarını temsil eder
    // dist, kaynaktan olan minimum mesafesini gösterir.
    int x, y, dist;
    dugum ileri;

    dugum(int x, int y, int dist) {
        this.x = x;
        this.y = y;
        this.dist = dist;
        ileri = null;
    }
};

public class kuyruk {

    dugum bas, son;
    

    public kuyruk() {

        bas = null;
        son = null;

    }

    public boolean bosmu() {
        return son == null;
    }

    void ekle(dugum yeni) {
        if (bosmu()) {
            bas = yeni;
            son = yeni;
        } else {
            son.ileri = yeni;
            son = yeni;

        }

    }

    dugum sil() {
        dugum tmp = bas;

        bas = bas.ileri;
        if (bas == null) {
            son = null;
        }
        return tmp;
    }
    // M x N matrix
    private static final int M = 10;
    private static final int N = 10;
    // Aşağıdaki diziler bir hücreden 4 olası hareketin tüm ayrıntılarını verir
    private static final int row[] = {-1, 0, 0, 1};
    private static final int col[] = {0, -1, 1, 0};
// Konuma gidip gitmediğini kontrol etme işlevi (satır, sütun)
// geçerli konumdan. İşlev false eğer döndürür (satır, sütun)
// geçerli bir konum değil veya 0 değeri var ya da zaten ziyaret edilmiş

                                                       
                                                            
    private static boolean gecerli(int mat[][], boolean ziyaret[][], int row, int col) {
        return (row >= 0) && (row < M) && (col >= 0) && (col < N)
                && mat[row][col] == 1 && !ziyaret[row][col];    // ziyaret  =visited
    }

    // Kaynaktan bir matris matında mümkün olan en kısa rotayı bulun
// hücre (i, j) hedef hücreye (x, y)
    
    
    
    
    public static void BFS(int mat[][], int i, int j, int x, int y) { //BFS= BREATH SEARCH ALGORİTM;

// ziyaret edilen hücreleri takip etmek için bir matris inşa et	
        boolean[][] ziyaret = new boolean[M][N];

        // boş bir kuyruk olustur
        
       kuyruk m = new kuyruk();

// kaynak hücreyi ziyaret edildiği gibi işaretle ve kaynak düğümü sıkıştır
        
        ziyaret[i][j] = true;
        
        m.ekle(new dugum(i, j, 0));
        
        // kaynaktan hedefe en uzun yolun uzunluğunu saklar
        
        int min_dist = Integer.MAX_VALUE;

        // sıra boş olmayana kadar calıstır
        
        while (!m.bosmu()) //!q.isEmpty()
        {
// kuyruktan ön düğümü aç ve işle
            
            dugum node = m.sil();

            // (i, j) mevcut hücreyi temsil eder ve dist
// kaynaktan minimum uzaklık
            i = node.x;
            j = node.y;
            
            int dist = node.dist;

            // eğer hedef bulunursa, min_dist'i güncelle ve durdur
            if (i == x && j == y) {
                min_dist = dist;
                break;
            }

            // mevcut hücreden tüm 4 olası hareketi kontrol et
// ve her geçerli hareketi zorla
            for (int k = 0; k < 4; k++) {
                // pozisyona gitmek mümkün mü kontrol edin
// (i + satır [k], j + col [k]) geçerli konumdan
                if (gecerli(mat, ziyaret, i + row[k], j + col[k])) {
                    
                    // bir sonraki hücreyi ziyaret edildi olarak işaretle ve sıkıştır
                    ziyaret[i + row[k]][j + col[k]] = true;
                    m.ekle(new dugum(i + row[k], j + col[k], dist+1));
                }
            }
        
        }
        if (min_dist != Integer.MAX_VALUE) {
            
            
            System.out.print("Kaynaktan hedefe giden en kısa yol "
                    + "has length == " + min_dist);
            
            
        } else {
            System.out.print("Hedefe belirli bir kaynaktan ulaşılamaz");
        }
    }

    //Labirentteki en kısa yol
    
    
    
    public static void main(String[] args) {
        
        // giriş labirenti
        int[][] mat
                = {
                    {1, 1, 1, 1, 1, 0, 0, 1, 1, 1},
                    {0, 1, 1, 1, 1, 1, 0, 1, 0, 1},
                    {0, 0, 1, 0, 1, 1, 1, 0, 0, 1},
                    {1, 0, 1, 1, 1, 0, 1, 1, 0, 1},
                    {0, 0, 0, 1, 0, 0, 0, 1, 1, 1},
                    {1, 0, 1, 1, 1, 0, 0, 1, 1, 0},
                    {0, 0, 0, 0, 1, 0, 0, 1, 0, 1},
                    {0, 1, 1, 1, 1, 1, 1, 1, 0, 0},
                    {1, 1, 1, 1, 1, 0, 0, 1, 1, 1},
                    {0, 0, 1, 0, 0, 1, 1, 0, 0, 1}
                };
// Kaynaktan (0, 0) en kısa yolu bul
// hedef (7, 5)
        BFS(mat, 0, 0, 9, 9);
    }
}

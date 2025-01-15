//
//  main.c
//  Rsa
//
//  Created by Ata yavuz Aydoğan on 15.01.2025.
//

#include <stdio.h>
#include <math.h>

void Rsa(void);

//asal kontrol
int asal (long long num){
    if(num <= 1 ) return 0;
    if (num <= 3) return 1;
    if(num % 2 == 0 || num % 3 == 0) return 0;
    for (int i = 5; i * i <= num; i += 6) {
        if (num % i == 0 || num % (i+2) == 0) {
            return 0;
        }
    }
    return 1;
}
// Genişletilmiş Öklid Algoritması
long long G_oklid(long long a, long long b, long long *x, long long *y) {
    if (a == 0) {
        *x = 0;
        *y = 1;
        return b;
    }

    long long x1, y1;
    long long gcd = G_oklid(b % a, a, &x1, &y1);

    *x = y1 - (b / a) * x1;
    *y = x1;

    return gcd;
}

// Modüler Ters Fonksiyonu
long long modular_ters(long long e, long long eu) {
    long long x, y;
    long long gcd = G_oklid(e, eu, &x, &y);

    // Modüler ters yalnızca gcd(e, eu) = 1 olduğunda vardır
    if (gcd != 1) {
        printf("Modüler ters mevcut degil, cünkü e ve eu aralarında asal degil.\n");
        return -1; // Başarısızlık durumu
    }

    // Negatif bir sonucu pozitif bir mod değeri ile düzelt
    long long mod = (x % eu + eu) % eu;
    return mod;
}
long long modular_us(long long base, long long exp, long long mod) {
    long long result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

void Rsa(void){
    long long p, q;
    // mod
    long long n;
    // eulerphi sayısı
    long long eu;
    // e sayısı
    long long e;
    // e -1 mod(eu) da
    long long m;
    // ciphertext
    long long ct;
    // plaintext
    long long pt;
    // Deşifrelenmiş
    long long dec;
    
    printf("q ve p sayıları asal olmak zorundadır\n");
    printf("Asal sayılar (q ve p) girin:\n");
    scanf("%lld %lld", &q, &p);

    if (!asal(q) || !asal(p)) {
        printf("Girilen sayılar asal değil!\n");
        return;
    }
        
    eu = (q - 1) * (p - 1);
    n = q * p;
    
    printf("1 ile %lld arasında bir sayı seçiniz ve sayı %lld ile aralarında asal olmak zorundadır\n",eu,eu);
    printf("e = ");
    scanf("%lld",&e);
    if (G_oklid(e, eu, &m, &m) != 1) {
        printf("e ve %lld aralarında asal değil!\n", eu);
        return;
    }

    m = modular_ters(e,eu);


    printf("Şifrelemek istediğiniz sayıyı girin: ");
    scanf("%lld", &pt);

    ct = modular_us(pt, e, n);
    printf("Şifreli metin: %lld\n", ct);

    dec = modular_us(ct, m, n);
    printf("Çözümlenmiş metin: %lld\n", dec);
        
}
int main(void) {
    Rsa();
    return 1;
}

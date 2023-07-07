# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown) ![](https://img.shields.io/badge/Additional_Coverage-Code_Review-purple)  <br/>

## Hash Calculation and Comparison

Assuming the file name is _hash.c_, then to compile _gcc hash.c -o hash -lssl -lcrypto_

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <openssl/evp.h>

void calculate_md5(const char* message, unsigned char* digest) {
    EVP_MD_CTX* context = EVP_MD_CTX_new();
    EVP_DigestInit(context, EVP_md5());
    EVP_DigestUpdate(context, message, strlen(message));
    EVP_DigestFinal(context, digest, NULL);
    EVP_MD_CTX_free(context);
}

int compare_hashes(const unsigned char* hash1, const unsigned char* hash2) {
    for (int i = 0; i < EVP_MD_size(EVP_md5()); i++) {
        if (hash1[i] != hash2[i]) {
            return 0;  // Hashes are different
        }
    }
    return 1;  // Hashes are the same
}

int main() {
    char message1[] = "Hello, 22CYS! Simple hash library using MD5";
    unsigned char digest1[EVP_MAX_MD_SIZE];
	unsigned char digest2[EVP_MAX_MD_SIZE];

    calculate_md5(message1, digest1);

    printf("MD5 hash code: ");
    for (int i = 0; i < EVP_MD_size(EVP_md5()); i++) {
        printf("%02x", digest1[i]);
    }
    printf("\n");
	
	char message2[] = "Hello, 22CYS! Simple hash library using MD4";
	calculate_md5(message2, digest2);
	
	printf("MD5 hash code: ");
    for (int i = 0; i < EVP_MD_size(EVP_md5()); i++) {
        printf("%02x", digest2[i]);
    }
    printf("\n");
	
	int result = compare_hashes(digest1, digest2);
    if (result) {
        printf("Hashes match!\n");
    } else {
        printf("Hashes do not match.\n");
    }

    return 0;
}
```

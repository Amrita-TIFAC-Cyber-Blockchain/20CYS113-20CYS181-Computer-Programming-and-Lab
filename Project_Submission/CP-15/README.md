# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_LINE_LENGTH 100

// Function to find and display IP address based on the given name in local_dns file
int findIPinLocalDNS(const char *name) {
    FILE *local_dns_file = fopen("local_dns.txt", "r");
    if (local_dns_file == NULL) {
        return 0; // Error occurred while opening local_dns file
    }

    char line[MAX_LINE_LENGTH];

    while (fgets(line, MAX_LINE_LENGTH, local_dns_file) != NULL) {
        char domain[MAX_LINE_LENGTH];
        char ip[MAX_LINE_LENGTH];

        if (sscanf(line, "%s %s", domain, ip) == 2) {
            if (strcmp(domain, name) == 0) {
                printf("IP Address for %s (from local_dns): %s\n", name, ip);
                fclose(local_dns_file);
                return 1; // Name found in local_dns file
            }
        }
    }

    fclose(local_dns_file);
    return 0; // Name not found in local_dns file
}

// Function to find and display IP address based on the given name in root file
int findIPinRoot(const char *tld, char *tld_server_ip) {
    FILE *root_file = fopen("root.txt", "r");
    if (root_file == NULL) {
        return 0; // Error occurred while opening root file
    }

    char line[MAX_LINE_LENGTH];

    while (fgets(line, MAX_LINE_LENGTH, root_file) != NULL) {
        char tld_name[MAX_LINE_LENGTH];
        char ip[MAX_LINE_LENGTH];

        if (sscanf(line, "%s %s", tld_name, ip) == 2) {
            if (strcmp(tld_name, tld) == 0) {
                strcpy(tld_server_ip, ip);
                fclose(root_file);
                return 1; // Found TLD server IP in root file
            }
        }
    }

    fclose(root_file);
    return 0; // TLD not found in root file
}

// Function to find and display IP address based on the given name in authoritative file
int findIPinAuthoritative(const char *tld_server_ip, const char *name) {
    char authoritative_file_name[MAX_LINE_LENGTH];
    snprintf(authoritative_file_name, sizeof(authoritative_file_name), "%s.txt", tld_server_ip);

    FILE *authoritative_file = fopen(authoritative_file_name, "r");
    if (authoritative_file == NULL) {
        return 0; // Error occurred while opening authoritative file
    }

    char line[MAX_LINE_LENGTH];

    while (fgets(line, MAX_LINE_LENGTH, authoritative_file) != NULL) {
        char domain[MAX_LINE_LENGTH];
        char ip[MAX_LINE_LENGTH];

        if (sscanf(line, "%s %s", domain, ip) == 2) {
            if (strcmp(domain, name) == 0) {
                printf("Searching in authoritative for %s...\n", name);
                printf("IP Address for %s: %s\n", name, ip);
                fclose(authoritative_file);
                return 1; // Name found in authoritative file
            }
        }
    }

    fclose(authoritative_file);
    return 0; // Name not found in authoritative file
}

// Function to update the local DNS file with a new entry
void updateLocalDNS(const char *name, const char *ip_address) {
    FILE *file = fopen("local_dns.txt", "a");
    if (file == NULL) {
        printf("Error opening the local_dns.txt file.\n");
        return;
    }

    fprintf(file, "%s %s\n", name, ip_address);
    fclose(file);
}

// Function to clear the content of local DNS file
void clearLocalDNS() {
    FILE *file = fopen("local_dns.txt", "w");
    if (file == NULL) {
        printf("Error opening the local_dns.txt file.\n");
        return;
    }

    fclose(file);
    printf("Local DNS cache cleared successfully.\n");
}

// Function to display the content of local DNS file
void displayLocalDNS() {
    FILE *file = fopen("local_dns.txt", "r");
    if (file == NULL) {
        printf("Error opening the local_dns.txt file.\n");
        return;
    }

    char line[MAX_LINE_LENGTH];
    printf("Local DNS cache:\n");

    while (fgets(line, MAX_LINE_LENGTH, file) != NULL) {
        printf("%s", line);
    }

    fclose(file);
}

// Function to log the message to the log file
void logMessage(const char *message) {
    FILE *log_file = fopen("dns_log.txt", "a");
    if (log_file == NULL) {
        printf("Error opening the dns_log.txt file.\n");
        return;
    }

    fprintf(log_file, "%s\n", message);
    fclose(log_file);
}

// Updated findAndDisplayIP function
void findAndDisplayIP(const char *name) {
    char log_message[MAX_LINE_LENGTH];
    snprintf(log_message, sizeof(log_message), "Searching in local_dns for %s...", name);
    logMessage(log_message);

    if (!findIPinLocalDNS(name)) {
        snprintf(log_message, sizeof(log_message), "Not found in local_dns. Searching in root for %s...", name);
        logMessage(log_message);

        char tld[MAX_LINE_LENGTH];
        if (sscanf(name, "%*[^.].%[^.]", tld) == 1) {
            char tld_server_ip[MAX_LINE_LENGTH];
            if (findIPinRoot(tld, tld_server_ip)) {
                // If TLD server IP found in root, search for the domain in authoritative
                snprintf(log_message, sizeof(log_message), "Found TLD server IP for %s. Now searching in authoritative...", name);
                logMessage(log_message);

                if (!findIPinAuthoritative(tld_server_ip, name)) {
                    snprintf(log_message, sizeof(log_message), "Name '%s' not found in the records.", name);
                    logMessage(log_message);
                } else {
                    updateLocalDNS(name, tld_server_ip);
                    snprintf(log_message, sizeof(log_message), "IP Address for %s found in authoritative. Updated in local_dns.", name);
                    logMessage(log_message);
                }
            } else {
                snprintf(log_message, sizeof(log_message), "TLD server IP not found in root for %s. Name not found in the records.", name);
                logMessage(log_message);
            }
        } else {
            snprintf(log_message, sizeof(log_message), "Invalid domain name format: %s", name);
            logMessage(log_message);
            printf("Invalid domain name format: %s\n", name);
        }
    }
}

// Function to handle the command line arguments
int handleCommand(int argc, char *argv[]) {
    if (argc < 2) {
        printf("Usage: %s <command>\n", argv[0]);
        printf("Commands:\n");
        printf("  dnslookup <domain_name>: Look up IP address for the given domain name.\n");
        printf("  flushdns: Clear the content of local DNS cache.\n");
        printf("  displaydns: Display the content of local DNS cache.\n");
        printf("  logfile: Show the log file with all the messages.\n");
        return 1;
    }

    char *command = argv[1];

    if (strcmp(command, "dnslookup") == 0) {
        if (argc != 3) {
            printf("Usage: %s dnslookup <domain_name>\n", argv[0]);
            return 1;
        }

        const char *domain_name = argv[2];
        findAndDisplayIP(domain_name);
    } else if (strcmp(command, "flushdns") == 0) {
        clearLocalDNS();
    } else if (strcmp(command, "displaydns") == 0) {
        displayLocalDNS();
    } else if (strcmp(command, "logfile") == 0) {
        printf("Log file contents:\n");
        FILE *log_file = fopen("dns_log.txt", "r");
        if (log_file == NULL) {
            printf("Error opening the dns_log.txt file.\n");
            return 1;
        }

        char line[MAX_LINE_LENGTH];

        while (fgets(line, MAX_LINE_LENGTH, log_file) != NULL) {
            printf("%s", line);
        }

        fclose(log_file);
    } else {
        printf("Invalid command. Use one of the following commands:\n");
        printf("  dnslookup <domain_name>\n");
        printf("  flushdns\n");
        printf("  displaydns\n");
        printf("  logfile\n");
        return 1;
    }

    return 0;
}

int main(int argc, char *argv[]) {
    int result = handleCommand(argc, argv);
    return result;
}
```

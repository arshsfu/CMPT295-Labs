#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>

#define HIST_SIZE 5

void add_to_hist(char *history[], int *count, char *line) {
  if (*count < HIST_SIZE) {
    history[*count] = line;
    (*count)++;
  } else {
    free(history[0]);

    for (int i = 1; i < HIST_SIZE; i++) {
      history[i - 1] = history[i];
    }
    history[HIST_SIZE - 1] = line;
  }
}

void print_history(char *history[], int count) {
  for (int i = 0; i < count; i++) {
    printf("%s", history[i]);
  }
}

int main(void) {
  char *history[HIST_SIZE] = {NULL};
  int count = 0;

  char *line = NULL;
  size_t len = 0;

  while (1) {
    printf("Enter input: ");
    fflush(stdout);

    ssize_t nread = getline(&line, &len, stdin);
    if (nread == -1) {
      break;
    }

    char *stored_line = malloc(strlen(line) + 1);
    if (!stored_line) {
      perror("malloc");
      break;
    }
    strcpy(stored_line, line);
    add_to_hist(history, &count, stored_line);

    if (strcmp(stored_line, "print\n") == 0) {
      print_history(history, count);
    }
  }

  for (int i = 0; i < count; i++) {
    free(history[i]);
  }
  free(line);

  return 0;
}

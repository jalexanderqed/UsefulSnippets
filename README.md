# UsefulSnippets
Useful bits of code I've written that might come in handy later.

## Efficient C method to read all input from command line, regardless of length

```
int getCommandLine(char **buff) {
    int count = 0;
    char *line = (char *) malloc(BLOCK_SIZE * sizeof(char));
    line[0] = '\0';
    if (line == NULL) {
        *buff = line;
        return -1;
    }

    bool done = false;

    while (!done) {
        if (fgets(count == 0 ? line : &(line[count * BLOCK_SIZE - 1]), count == 0 ? BLOCK_SIZE : BLOCK_SIZE + 1,
                  stdin) == NULL) {
            *buff = line;
            if(line[0] == '\0')
                return -1;
            else
                done = true;
        }
        else {
            if (line[strlen(line) - 1] == '\n') {
                done = true;
            }
        }

        if (!done) {
            count++;
            if ((line = realloc(line, (count + 1) * BLOCK_SIZE * sizeof(char))) == NULL) return -1;
        }
    }

    *buff = line;

    return (count + 1) * BLOCK_SIZE;
}
```

#include <stdio.h>
#include <string.h>

int main()
{
    char str[100];
    int i, n, state[3] = {0, 0, 0};
    int next[3];

    printf("Enter a string over {o, 1}: ");
    scanf("%99s", str);

    n = strlen(str);

    if (n == 0 || str[0] != 'o')
    {
        printf("String rejected\n");
        return 0;
    }

    state[0] = 1;  /* Initial state q0 */

    for (i = 0; i < n; i++)
    {
        if (str[i] != 'o' && str[i] != '1')
        {
            printf("Invalid string\n");
            return 0;
        }

        next[0] = next[1] = next[2] = 0;

        if (state[0])
        {
            if (str[i] == 'o')
                next[1] = 1;
        }

        if (state[1])
        {
            if (str[i] == 'o')
                next[1] = 1;
            else
                next[1] = 1, next[2] = 1;
        }

        if (state[2])
        {
            /* No outgoing transitions from final state */
        }

        for (int j = 0; j < 3; j++)
            state[j] = next[j];
    }

    if (state[2])
        printf("String accepted\n");
    else
        printf("String rejected\n");

    return 0;
}

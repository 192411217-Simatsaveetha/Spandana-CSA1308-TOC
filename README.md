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
#include <stdio.h>

int main()
{
    int n, m, i, j, u, v;
    int e[20][20] = {0};
    int closure[20][20] = {0};
    int changed;

    printf("Enter number of states: ");
    scanf("%d", &n);

    printf("Enter number of epsilon transitions: ");
    scanf("%d", &m);

    printf("Enter transitions (from to):\n");
    for (i = 0; i < m; i++)
    {
        scanf("%d %d", &u, &v);
        e[u][v] = 1;
    }

    for (i = 0; i < n; i++)
    {
        closure[i][i] = 1;

        for (j = 0; j < n; j++)
            closure[i][j] = closure[i][j] || e[i][j];
    }

    do
    {
        changed = 0;

        for (i = 0; i < n; i++)
        {
            for (j = 0; j < n; j++)
            {
                if (closure[i][j])
                {
                    for (int k = 0; k < n; k++)
                    {
                        if (e[j][k] && !closure[i][k])
                        {
                            closure[i][k] = 1;
                            changed = 1;
                        }
                    }
                }
            }
        }
    } while (changed);

    printf("\nEpsilon-closures:\n");

    for (i = 0; i < n; i++)
    {
        printf("E-closure(q%d) = { ", i);

        for (j = 0; j < n; j++)
        {
            if (closure[i][j])
                printf("q%d ", j);
        }

        printf("}\n");
    }

    return 0;
}

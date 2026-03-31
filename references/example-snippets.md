# Example Snippets

Use these as calibration examples or seed patterns. Do not repeat them verbatim too often.

## Level 1 example

```c
#include <string.h>

int copy_word(char *dst, size_t dst_size, const char *src) {
    size_t len = strcspn(src, " ");
    if (len > dst_size) {
        return -1;
    }
    memcpy(dst, src, len);
    dst[len] = '\0';
    return 0;
}
```

Primary issue: off-by-one destination check. If `len == dst_size`, terminator write is out of bounds.

## Level 2 example

```c
#include <stdlib.h>
#include <string.h>

typedef struct {
    char *name;
    char *desc;
} item_t;

int item_copy(item_t *dst, const item_t *src) {
    *dst = *src;

    if (src->name) {
        dst->name = malloc(strlen(src->name) + 1);
        if (!dst->name) {
            return -1;
        }
        strcpy(dst->name, src->name);
    }

    if (src->desc) {
        dst->desc = malloc(strlen(src->desc) + 1);
        if (!dst->desc) {
            free(dst->name);
            return -1;
        }
        strcpy(dst->desc, src->desc);
    }

    return 0;
}
```

Primary issue: shallow-copy start plus unsafe failure semantics leaves `dst` in a partially copied/unsafe state.

## Pointer-to-pointer example

```c
#include <stdlib.h>
#include <string.h>

int append_exclamation(char **dst) {
    size_t len = strlen(*dst);
    char *tmp = realloc(*dst, len + 2);
    if (!tmp) {
        return -1;
    }

    tmp[len] = '!';
    tmp[len + 1] = '\0';
    return 0;
}
```

Primary issue: fails to assign `*dst = tmp` after realloc.

## Cleanup-path example

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    char *name;
    FILE *fp;
} resource_t;

int resource_init(resource_t *r, const char *name, const char *path) {
    r->name = malloc(strlen(name) + 1);
    if (!r->name) {
        return -1;
    }
    strcpy(r->name, name);

    r->fp = fopen(path, "r");
    if (!r->fp) {
        return -1;
    }

    return 0;
}
```

Primary issue: if `fopen` fails, the function leaks `r->name` on the error path.

## Validation example

```c
#include <string.h>

int has_suffix(const char *name, const char *suffix) {
    size_t name_len = strlen(name);
    size_t suffix_len = strlen(suffix);

    return strcmp(name + (name_len - suffix_len), suffix) == 0;
}
```

Primary issue: if `suffix_len > name_len`, the subtraction underflows and the pointer passed to `strcmp` becomes invalid.

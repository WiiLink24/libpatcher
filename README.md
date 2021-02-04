# libpatcher

libpatcher provides a solution to easily apply several common IOS patches.
It can be used to automate enabling AHBPROT by reloading IOS with the ES ticket patch,
to apply the negation of ISFS permissions, and to disable signature verification within ES.

For example, an application requiring usage of ES_Identify would require all of the above
in order to load a ticket and TMD manually, and then truly identify.

Such an application could reduce patching to:

```c
int main(void) {
    VIDEO_Init();
    // [continue with video initialization]

    bool success = apply_patches();
    if (!success) {
        printf("Failed to apply patches!\n");
    }

    WPAD_Init();
    // [...]
}
```

It's recommended to not initialize WPAD and similar IOS-backed functions until after patching,
as IOS upon reload will not be set up to relay input over Bluetooth.

Alternatively, one can shutdown, patch, and later initialize WPAD and similar libraries.

ES will be automatically initialized by libogc upon IOS reload.

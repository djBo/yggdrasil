# Minimal.db

With the LambdaMOO server comes a tiny database called *minimal.db*. It is just enough to boot-strap a new core. On closer inspection, it also becomes clear that the initial structure doesn't match LambdaCore as their Wizard is actually object #2 and not #3.

Let's take a crack at it anyways, and see where it might lead. The remainder of the document expects you to setup your own LambdaMOO server using the minimal.db as a starting point. 

## Bootstrap

Let's take Pavel's advise, and begin by programming the initial room's `eval` verb with a simple (but a tad fancy) MOO-code expression evaluator:

```moo
.program here:eval
answer = eval("return " + argstr + ";");
if (answer[1])
  notify(player, tostr("=> ", toliteral(answer[2])));
else
  for line in (answer[2])
    notify(player, line);
  endfor
endif
.
```

With this in place, we can now execute built-in functions directly, albeit limited to one-liner commands (for now). By using the semi-colon `;` prefix, we can keep our commands shorter too.

#### Making the Wizard object #2

While you could, in theory (and practice, I tried), perform this change straight into the database file, this is not recommended. Besides, we can do the switcheroo right from the moo! The following flow should be executed right after bootstrapping:

1. Let's create a new object:
    ```
    ;create(#1, #3)
    ```

2. Name it "*The First Room*":
    ```
    ;#4.name = "The First Room"
    ```

3.  Add the `eval` verb to it:
    ```
    ;add_verb(#4, {#3, "d", "eval"}, {"any", "any", "any"})
    ```

4. Program it with the same bootstrap code above:
    ```
    .program #4:eval
    ...
    .
    ```

5. Move yourself to the new room:
    ```
    ;move(#3, #4)
    ```

6. Re-program `#0:do_login_command` to return the updated Wizard object number:
    ```
    .program #0:do_login_command
    return #2;
    .
    ```

7. Recycle the initial room:
    ```
    ;recycle(#2)
    ```

8. Renumber yourself, this will disconnect you as you are being recycled:
    ```
    ;renumber(#3)
    ```

9. Reconnect and renumber the room:
    ```
    ;renumber(#4)
    ```

10. Clear the recycles obect #4:
    ```
    ;reset_max_object()
    ```

With this done, we are ready to continue onwards in our journey of the minimal.

Different Tech has different ways of accepting the parameter passed. This is because there is no RFC or anything defined for this.

- We usually see this in loads of Password reset functionality that if we send a requests with multiple `email` then only the first one is considered.

    ```html
    email=victim.com&email=attacker.com
    ```

- If in the URL the & or any other character is not encoded then the possibility is high that if you add a new value then it will be accepted.
- PHP usually consider the `last` occurrence

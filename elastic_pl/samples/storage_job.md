# ePL\_Storage\_job

{% code-tabs %}
{% code-tabs-item title="\#storage\_job" %}
```c
array_uint   1000;
submit_sz 1
submit_idx 0

function verify {
    u[0]=m[0];
    u[1]=m[1];
    u[2]=s[0];
    if(u[2]==0) u[2]=4000;
    verify_bty (u[0]<u[2]);
    verify_pow (u[0],u[1],u[2],u[3]);
}

function main {
    verify();
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% page-ref page="bitcoin\_mining.md" %}

>


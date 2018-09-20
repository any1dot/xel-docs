# ePL\_Simple\_job

{% code-tabs %}
{% code-tabs-item title="\#simple\_job" %}
```c
   1000;

function verify {
    u[0]=m[0];
    u[1]=m[1];
    verify_bty (u[0]<1000);
    verify_pow (u[0],u[1],u[2],u[3]);
}

function main {
    verify();
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% page-ref page="storage\_job.md" %}

>


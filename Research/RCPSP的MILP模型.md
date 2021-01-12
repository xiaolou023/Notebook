# RCPSP

## Time-indexed formulations

**binary start time variables**

$x_{it}$ = 1 if and only if activity $i$ starts at time $t$.
$$
\begin{array}{ll}
{\text { Min}} & {\sum_{t \in H} t x_{n+1, t}} \\
{\text { s.t. }} & {\sum_{t \in H} t x_{j t}-\sum_{t \in H} t x_{i t} \geq p_{i} \quad((i, j) \in E)} \\
%{} & {\sum_{\tau=0}^{t-p_{i}} x_{i \tau}-\sum_{\tau=0}^{t} x_{j \tau} \geq 0 \quad((i, j) \in E ; t \in H)} \\
{} & {\sum_{i \in V} \sum_{\tau=t-p_{i}+1}^{t} r_{i k} x_{i \tau} \leq R_{k} \quad(t \in H ; k \in \mathscr{R})} \\
{} & {\sum_{t \in H} x_{i t}=1 \quad(i \in V)} \\ {} & {x_{i t}=0 \quad\left(i \in V ; t \in H^{+} \backslash\left\{E S_{i}, \ldots, L S_{i}\right\}\right)} \\
{} & {x_{i t} \in\{0,1\} \quad\left(i \in V ; t \in\left\{E S_{i}, \ldots, L S_{i}\right\}\right)}
\end{array}
$$


**binary start step variables**

$\xi_{it}$ = 1 if and only if activity $i$ starts at time $t$ or before.
$$
\begin{array}{ll}
{\operatorname{Min}} & {\sum_{t \in H} t\left(\xi_{n+1, t}-\xi_{n+1, t-1}\right)} \\ 
{\text { s.t. }} & {\xi_{i, t-p_{i}}-\xi_{j t} \geq 0 \quad((i, j) \in E ; t \in H)} \\
{} & {\sum_{i \in V} r_{i k}\left(\xi_{i t}-\xi_{i, t-p_{i}}\right) \leq R_{k} \quad(t \in H ; k \in \mathscr{R})} \\ {} & {\xi_{i, L S_{i}}=1 \quad(i \in V)} \\
{} & {\xi_{i t}-\xi_{i, t-1} \geq 0 \quad(i \in V ; t \in H)} \\
{} & {\xi_{i t}=0 \quad\left(i \in V ; t \in H^{+}, t \leq E S_{i}-1\right)} \\
{} & {\xi_{i t} \in\{0,1\} \quad\left(i \in V ; t \in\left\{E S_{i}, \ldots, L S_{i}-1\right\}\right)}
\end{array}
$$
**binary _on/off_ variables**

$\mu_{it}$ = 1 if activity $i$ is in process at time $t$. 
$$
\begin{array}{ll}
{\operatorname{Min}} & {\sum_{t \in H} t\left(\mu_{n+1, t}-\mu_{n+1, t-1}\right)} \\ 
{\text { s.t. }} & {\sum_{\alpha=0}^{K_{i, t}-p_{i}} \mu_{i, t-(\alpha+1) p_{i}}-\sum_{\alpha=0}^{K_{j, t}} \mu_{j, t-\alpha p_{j}} \geq 0 \quad((i, j) \in E ; t \in H)} \\
{} & {\sum_{\alpha=0}^{K_{i, t-(\alpha+1) p_{i}}} \mu_{j, t-\alpha p_{j}} \geq 0 \quad((i, j) \in E ; t \in H)} \\
{} & {\sum_{i \in V, p_{i}>0} r_{i k} \mu_{i t} \leq R_{k} \quad(t \in H ; k \in \mathscr{R})} \\
{} & {\sum_{\alpha=0}^{K_{i},c_{i}-\phi(i)} \mu_{i, L C_{i}-\phi(i)-\alpha p_{i}}=1 \quad(i \in V)} \\
{} & {\sum_{\alpha=0}^{K_{i t}} \mu_{i, t-\alpha p_{i}}-\sum_{\alpha=0}^{K_{i, t-1}} \mu_{i, t-\alpha p_{i}-1} \geq 0 \quad(i \in V ; t \in H \backslash\{0\})} \\
{} & {\mu_{i t}=0} \quad {(i \in V ; t \in Z(i))} \\
{} & {\mu_{i t} \in\{0,1\}} \quad {(i \in V ; t \in U(i))} \\
{where} & {\phi(i)=1 \text { if } p_{i} \geq 1 \text { and } \phi(i)=0 \text { if } p_{i}=0}
\end{array}
$$

## Chain-decomposition formulation

$$
\begin{array}{ll}
{\text { Min }} & C_{\text {max}} \\
{\text { s.t. }} & {C_{\max } \geq \sum_{s \in \mathscr{S}_{P}} C_{s P} \beta_{s P} \quad(P \in \mathscr{P})} \\
{} & {\sum_{s \in \mathscr{S}_{P}} \beta_{s P}=1 \quad(P \in \mathscr{P})} \\
{} & {\sum_{t=E C_{i}}^{L C_{i}} t\left(\sum_{s \in \mathscr{F}_{P(i)}} a_{i t s P(i)} \beta_{s P(i)}-\sum_{s \in \mathscr{F}_{p}} a_{i t s P} \beta_{s P}\right) \quad(i \in V ; P \in \mathscr{P} \backslash P(i))} \\
{} & {\sum_{i \in V} \sum_{\tau=t}^{t+p_{i}-1} \sum_{s \in \mathscr{P}_{P(i)}} r_{i k} a_{i \tau s P(i)} \beta_{s P(i)} \leq R_{k} \quad(k \in \mathscr{R} ; t \in H)} \\
{} & {\beta_{s P} \in\{0,1\} \quad\left(P \in \mathscr{P} ; s \in \mathscr{P}_{P}\right)} 
\end{array}
$$

## Sequencing formulation

$$
\begin{array}{ll}
{\text{Min}} & S_{n+1} \\
{\text { s.t.} } & {z_{i j}+z_{ji} \leq 1 \quad (i, j \in V, i<j)} \\
{} & {z_{i j}+z_{j h}-z_{i h} \leq 1 \quad (i, j, h \in V, i \neq j \neq h)} \\
{} & {z_{i j}=1 \quad ((i, j) \in E)} \\
{} & {S_{j}-S_{i}-M_{i j} z_{i j} \geq p_{i}-M_{i j} \quad(i, j \in V, i \neq j)} \\
{} & \sum_{i, j \in F,i \neq j} z_{ij} \geq 1 \quad (F \in \mathscr{F}) \\
{} & {z_{i j} \in\{0,1\} \quad(i, j \in V, i \neq j)} \\
{} & {E S_{i} \leq S_{i} \leq L S_{i} \quad(i \in V)} \\
{where} & {\mathscr{F} \text { denotes the set of all minimal forbidden sets }}
\end{array}
$$

## Flow based formulation

$$
\begin{array}{l}
{\ldots} \\
{\phi_{i j}^{k}-\min \left(\tilde{r}_{i k}, \tilde{r}_{j k}\right) z_{i j} \leq 0 \quad(i, j \in V, i \neq j ; k \in \mathscr{R})} \\
{\sum_{j \in V \backslash\{i\}} \phi_{i j}^{k}=\tilde{r}_{i k} \quad(i \in V \backslash\{n+1\})} \\
{\sum_{i \in V \backslash\{j\}} \phi_{i j}^{k}=\tilde{r}_{j k} \quad(j \in V \backslash\{0\})} \\
{0 \leq \phi_{i j}^{k} \leq \min \left(\tilde{r}_{i k}, \tilde{r}_{j k}\right) \quad(i, j \in V, i \neq n+1, j \neq 0, i \neq j ; k \in \mathscr{R})}
\end{array}
$$

## Event based formulation

$$
\begin{array}{ll}
{\text { Min } t_{n}} & {} \\
{\text { s.t. }} & {t_{0}=0} \\
{} & {t_{e+1}-t_{e} \geq 0 \quad(e \in \mathscr{E} \backslash\{n\})} \\
{} & {t_{f}-t_{e}-p_{i} a_{i e}^{+}+p_{i}\left(1-a_{i f}^{-}\right) \geq 0 \quad(i \in V ; e, f \in \mathscr{E}, e<f)} \\
{} & {\sum_{e \in \mathcal{E}} a_{i e}^{+}=1 \quad(i \in V)} \\
{} & {\sum_{e \in \mathcal{E}} a_{i v}^{-}+\sum_{v=e}^{n} a_{i v}^{+} \leq 1 \quad(i \in V ; e \in \mathscr{E})} \\
{} & {\sum_{e^{\prime}=e}^{n} a_{i e^{\prime}}^{-}+\sum_{e^{\prime}=0}^{e-1} a_{j e^{\prime}}^{+} \leq 1 \quad((i, j) \in E ; e \in \mathscr{E})} \\
{} & {b_{0 k}-\sum_{i \in V} r_{i k} a_{i 0}^{+}=0 \quad(k \in \mathscr{R})} \\
{} & {b_{e k}-b_{e-1, k}+\sum_{i \in V} r_{i k}\left(a_{i e}^{-}-a_{i e}^{+}\right)=0 \quad(e \in \mathscr{E} \backslash\{0\} ; k \in \mathscr{R})} \\
{} & {b_{e k} \leq R_{k} \quad(e \in \mathscr{E} ; k \in \mathscr{R})} \\
{} & {E S_{i} a_{i e}^{+} \leq t_{e} \leq L S_{i} a_{i e}^{+}+L S_{n+1}\left(1-a_{i e}^{+}\right) \quad(i \in V ; e \in \mathscr{E})} \\
{} & {\left(E S_{i}+p_{i}\right) a_{i e}^{-} \leq t_{e}(i \in V ; e \in \mathscr{E})} \\
{} & {t_{e} \leq \left(L S_{i}+p_{i}\right) a_{i e}^{-}+L S_{n+1}\left(1-a_{i e}^{-}\right)} \\
{} & {E S_{n+1} \leq t_{n}} \\
{} & {a_{i e}^{+}, a_{i e}^{-} \in\{0,1\} \quad(i \in V ; e \in \mathscr{E})} \\
{} & {t_{e} \geq 0 \quad(e \in \mathscr{E})} \\
{} & {b_{e k} \geq 0 \quad(e \in \mathscr{E} ; k \in \mathscr{R})}  
\end{array}
$$



## Constraint programming formulations

$$
\begin{array}{ll}
{\text{Min}} & \texttt{endOf}({n+1}) \\
{\text { s.t.} } & {\texttt{endBeforeStart}(i, j)} \quad \forall(i,j) \in P \\
{} & {\sum_{i \in V, r_{ik} > 0} \texttt{pulse}(i, r_{ik}) \leq R_k \quad \forall k \in R} \\
{} & {\texttt{length}(i) = p_i} \quad \forall i \in V
\end{array}
$$
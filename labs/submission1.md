# Lab 1 Submission

**Student:** Iukharev Roman 
**Repository (fork):** https://github.com/Corbonat/DevOps-Intro 

---

## Task 1 — SSH Commit Signature Verification

### 1.1 Why signed commits matter

Signed commits are important because they provide:

- *Authenticity* — confirms who created the commit.
- *Integrity* — confirms commit content was not changed after signing.
- *Traceability* — improves security in team workflows.

In DevOps, this is critical for trust in CI/CD pipelines, code reviews, and release history.

### 1.2 Why commit signing is important in DevOps workflows

DevOps teams collaborate quickly and often across many contributors.  
Commit signing reduces the risk of spoofed authorship and unauthorized changes, making the software delivery process safer and more auditable.

### 1.3 Evidence

**Verified badge on GitHub commit:**

![Verified commit](img/Verified_commit.png)

**SSH signing key added in GitHub account:**

![SSH key added](img/SSH_key_added.png)

---

## Task 2 — PR Template & Checklist

### 2.1 PR template setup

I created a PR template at:

- `.github/pull_request_template.md`

The template includes sections:

- Goal
- Changes
- Testing

And checklist items:

- Clear, descriptive PR title
- Documentation/README updated (if needed)
- No secrets or large temporary files committed

### 2.2 Evidence of template in `main`

Proof that `.github/pull_request_template.md` exists on `main` branch of my fork:

![PR template exists on main](img/Proof_of_PR_template_existing.png)

### 2.3 Evidence of auto-filled PR description

When opening a PR from `feature/lab1` to `main` in my fork, GitHub auto-filled the PR description from the template:

![PR auto-fill](img/PR_autofill.png)

### 2.4 How PR templates improve collaboration

PR templates improve collaboration by standardizing information in every pull request.  
Reviewers get consistent context (goal, changes, testing), which speeds up review and minimizes questions.  
Checklists also help prevent common mistakes, such as missing documentation updates.

### 2.5 Challenges encountered

- Initially confusing branch flow (`main` vs `feature/lab1`).
- After fixing branch workflow, the template and signed commits worked as expected.
- Accedently wrote the wrong commit (Commited adding a .png file as changing submission1.md)
---

## Final Status

- [x] Task 1 done
- [x] Task 2 done

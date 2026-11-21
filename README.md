# Two-Site University Hospital Network

Technical documentation for the Black Sun Empire (BSE) Cisco Packet Tracer network project. The design models a university hospital with sites in Alexandria and Cairo connected through a simulated ISP.

## Team

- Abdelrahman Mohamed Ramadan
- Abdelrahman Namir Ahmed Abdelkader
- Youssef Tarek Ibrahim Shaker

**Course:** CCNA  
**Instructor:** Mohamed Abdalla

## Documentation

The report explains the network design and summarizes its verification evidence. Device configurations are kept in the submitted Packet Tracer project file rather than reproduced as command listings in the report.

The report covers:

1. Introduction, scope, and requirements
2. Topology and device inventory
3. VLSM subnetting
4. Layer 2 design
5. Router-on-a-Stick and HSRP
6. Network services
7. Routing
8. Internet access and NAT
9. Security and management
10. FTP configuration backups
11. Verification summary
12. Conclusion and lessons learned

## Project files

```text
main.tex             LaTeX entry point
main.pdf             Compiled report
REPORT.md            Build checks and evidence audit
sections/             Section source files
figures/              Screenshots used in the report
tikz/                 Supplied TikZ diagrams
```

The submitted `.pkt` file contains the Packet Tracer implementation and is distributed separately.

## Build the PDF

Build with pdfLaTeX using `latexmk`:

```bash
latexmk -pdf -interaction=nonstopmode -halt-on-error main.tex
```

Alternatively, run pdfLaTeX from this directory more than once so the table of contents, figure list, and cross-references update:

```bash
pdflatex main.tex
pdflatex main.tex
```

Required LaTeX packages include `graphicx`, `booktabs`, `longtable`, `tabularx`, `caption`, `float`, `hyperref`, `cleveref`, `xcolor`, `geometry`, `fancyhdr`, and `tikz`.

## Evidence and checks

Screenshots in `figures/` document the topology and observed verification outputs. The report also records checks performed in the Packet Tracer file. `REPORT.md` summarizes the subnet validation, compilation, evidence review, and source observations.

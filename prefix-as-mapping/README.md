# README

## Instructions

Simply run the code provided in the Jupyter notebook `monte_carlo.ipynb`.

As input data, the notebook relies on the CSV file
`data/reachable-nodes-annotated-2024-01-25.csv`, which contains a list of reachable
nodes' addresses and network type (i.e., IPv4 or IPv6) obtained with
[p2p-crawler](https://github.com/virtu/p2p-crawler) as well as netgroup data (determined
in line with Bitcoin Core's strategy) and autonomous system number (determined using a
[kartograf](https://github.com/fjahr/kartograf)-generated ASMAP).

## Trustworthiness of input data

Reviewers don't have to rely on the autonomous system data provided in
`reachable-nodes-annotated-2024-01-25.csv`. The autonomous system numbers (ASN) for each
reachable node can be reproduced by running the code provided in
`reproduce_input_data.ipynb`, which uses an ASMAP generated with
[kartograf](https://github.com/fjahr/kartograf) on January 25, 2024 to map reachable
nodes' addresses to ASN.

In case of extreme paranoia, reviewers may generate their own ASMAP, and use
reachable-node data from other sources (e.g., [bitnodes](https://bitnodes.io)).

## Files

| File | Contents |
| --- | --- |
| `reproduce_input_data.ipynb` | A Jupyter notebook to annotate netgroup and autonomous system number information for each reachable Bitcoin node listed in `asmap-kartograf-2024-01-25.txt.bz2` |
| `monte_carlo.ipynb.` | A Jupyter notebook to carry out a Monte Carlo simulation of selecting ten random netgroups (taking netgroup sizes into account) and determining how many unique autonomous systems these netgroups correspond to. |
| `data/reachable-nodes-2024-01-25.csv` | CSV file containing a list of Bitcoin nodes reachable via clearnet on January 25, 2024, along with the nodes network types (i.e., IPv4 or IPv6) |
| `data/reachable-nodes-2023-02-06.csv` | CSV file containing a list of Bitcoin nodes reachable via clearnet on February 6, 2023, along with the nodes network types (i.e., IPv4 or IPv6) |
| `reachable-nodes-annotated-2024-01-25.csv` | CSV containing data from `reachable-nodes-2024-01-24.csv`, along with nodes' netgroup and autonomous system number. Netgroup and autonomous system data was added via `reproduce_input_data.ipynb`.|
| `reachable-nodes-annotated-2023-02-06.csv` | CSV containing data from `reachable-nodes-2023-02-06.csv`, along with nodes' netgroup and autonomous system number. Netgroup and autonomous system data was added via `reproduce_input_data.ipynb`.|
| `asmap-kartograf-2024-01-25.txt.bz2` | An ASMAP file, containing mappings of IPv4 and IPv6 subnets to autonomous system numbers, generated using [kartograf](https://github.com/fjahr/kartograf) on January 25, 2024. |
| `asmap-kartograf-2023-02-06.txt.bz2` | An ASMAP file, containing mappings of IPv4 and IPv6 subnets to autonomous system numbers, generated using [kartograf](https://github.com/fjahr/kartograf) on Februar 6, 2023. |

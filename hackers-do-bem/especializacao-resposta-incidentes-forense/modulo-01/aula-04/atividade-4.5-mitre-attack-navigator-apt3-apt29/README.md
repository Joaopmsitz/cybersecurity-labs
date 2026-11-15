# Activity 4.5 — MITRE ATT&CK Navigator: APT3 and APT29

## Objective

Use MITRE ATT&CK Navigator to compare the techniques associated with two threat groups, APT3 and APT29.

The exercise creates an individual layer for each group, assigns scores to the selected techniques, and combines the layers using the expression `a+b`.

## Tool and references

- [MITRE ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)
- [MITRE ATT&CK — APT3 (G0022)](https://attack.mitre.org/groups/G0022/)
- [MITRE ATT&CK — APT29 (G0016)](https://attack.mitre.org/groups/G0016/)

## 1. Create the APT3 layer

1. Open MITRE ATT&CK Navigator.
2. Select **Create New Layer**.
3. Choose **Enterprise ATT&CK**.
4. Open **Layer Information Settings**.
5. Rename the layer to `APT3`.
6. Open **Selection Controls**.
7. Select the search and multiselect option.
8. Choose **Threat Groups**.
9. Search for and select `APT3`.
10. Confirm the selection so that the techniques associated with the group are highlighted.

The group is identified in MITRE ATT&CK as **G0022**. The MITRE group profile describes APT3 as a China-based threat group attributed by researchers to China's Ministry of State Security.

## 2. Configure the APT3 layer

After selecting the group:

- Assign a background color to the selected techniques using **Technique Controls**.
- Open **Scoring**.
- Assign a score of `3` to indicate high relevance in the exercise.

The score is an analytical value used for the activity's comparison. It is not an intrinsic severity rating assigned by MITRE to the threat group.

## 3. Create the APT29 layer

1. Create another **Enterprise ATT&CK** layer.
2. Rename it to `APT29`.
3. Open **Selection Controls**.
4. Select the search and multiselect option.
5. Choose **Threat Groups**.
6. Search for and select `APT29`.
7. Confirm the selection.

APT29 is identified in MITRE ATT&CK as **G0016**. Its profile describes the group as attributed to Russia's Foreign Intelligence Service (SVR).

## 4. Configure the APT29 layer

For the second layer:

- Assign a background color different from the one used for APT3.
- Open **Scoring**.
- Assign a score of `2`, indicating medium relevance in the exercise.

The two layers now represent separate group selections with different visual colors and scoring values.

## 5. Combine the layers

The final activity step combines the two layers.

1. Select the option to create a layer from other layers.
2. Select the Enterprise ATT&CK version specified by the exercise: `Enterprise ATT&CK v17`.
3. Include the APT3 and APT29 layers.
4. Set the Score Expression to:

    a+b

5. Create the combined layer.

The expression adds the scores from the two source layers. A technique selected in both layers can therefore receive the sum of both scores, while a technique present in only one source layer retains the contribution from that layer.

## 6. Score interpretation

The exercise uses the following scale:

| Score | Interpretation |
|---:|---|
| 0 | Not applicable or not considered concerning |
| 1 | Low impact or relevance |
| 2 | Medium impact or relevance |
| 3 | High impact or relevance |

The activity assigned:

| Layer | Threat group | Score |
|---|---|---:|
| APT3 | G0022 | 3 |
| APT29 | G0016 | 2 |

The resulting layer provides a visual comparison of the techniques selected for the two groups.

## 7. Technical analysis

ATT&CK Navigator layers support visual analysis of adversary techniques and help security teams organize threat-informed defensive work.

Combining layers makes it easier to inspect:

- Techniques selected for both groups.
- Techniques selected for only one of the groups.
- Relative scores assigned by the analyst.
- Areas that may deserve additional monitoring, detection engineering, or threat-hunting attention.

The resulting visualization should be interpreted as a comparison based on the selected ATT&CK data and the scoring choices configured in the exercise. It does not prove that a group used every highlighted technique in every campaign or that the same technique has identical relevance in every organization.

## Result

The APT3 and APT29 layers were created, assigned different colors and scores, and combined using the expression `a+b`.

The combined layer is the final result captured for the activity.

## Evidence

[View Universal Class Evidence PDF — Page 4](../evidences.pdf)

## References

- [MITRE ATT&CK — APT3](https://attack.mitre.org/groups/G0022/)
- [MITRE ATT&CK — APT29](https://attack.mitre.org/groups/G0016/)
- [MITRE ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)

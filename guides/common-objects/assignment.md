# Assignment

| Parameter | Type             | Required | Description                                                                                                                                                                                                                                                                                             |
| :-------- | :--------------- | :------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| site_id   | string           | Yes      | Id of the Site that is assigned to the Operator. The admin adding or updating the Operator must have access to the Site.                                                                                                                                                                                |
| team_ids  | array of strings | No       | An array of team IDs that are assigned to the Operator. The assigned Teams must belonged to the Site, otherwise a validation error is returned. If `team_ids` is not specified, then Operator will be assigned to the `General` team. The provided team IDs will replace the existing team assignments. |
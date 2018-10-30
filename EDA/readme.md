Remove the features with small proportion of data
---------

# df.count() does not include NaN values
df_enough = df[[column for column in df if df[column].count() / len(df) >= 0.3]]
print("List of dropped columns:", end=" ")
for c in df.columns:
    if c not in df_enough.columns:
        print(c, end=", ")
print('\n')
df = df_enough

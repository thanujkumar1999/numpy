import pandas as pd
a = pd.DataFrame({"A": pd.array(['a', 'b'], dtype=pd.StringDtype("pyarrow"))})
a2 = pd.DataFrame({"A": pd.array(['a', 'b'], dtype=pd.StringDtype("python"))})

a.to_parquet("test.parquet")
with pd.option_context("string_storage", "pyarrow"):
    b = pd.read_parquet("test.parquet")
pd.testing.assert_frame_equal(b, a)

a2.to_parquet("test.parquet")
with pd.option_context("string_storage", "pyarrow"):
    b = pd.read_parquet("test.parquet")
pd.testing.assert_frame_equal(b, a)

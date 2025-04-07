# structural_variance

## Project directory layout:
```
your_pipeline/
├── bin/
│   └── nextflow_extract_coordinates.py     ← processing vcf files
├── main.nf                        ← Nextflow workflow file
├── nextflow.config               ← pipeline configuration
├── data/
│   ├── HG002_merged.vcf
│   └── supp_vec_to_tool_map.json
└── output/
```



## Extract Structural Variant Coordinates (SV) from VCF into BED Files (nextflow_extract_coordinates.py)
This tool processes a merged VCF file to extract structural variant (SV) coordinates and saves them into BED files, with separate files for each tool (e.g., Delly, Manta, Smoove) based on the SUPP_VEC field.

Requirements:
- Python 3.x
Dependencies:
- pysam (for handling VCF files)
- json (for mapping support vector to tools)
- csv (for writing BED files)
- Create a supp_vec_to_tool_map.json file (explained below).

Input:
- vcf (VCF file to process)
- output_prefix (Prefix for output BED files)
- supp_vec_map (JSON file mapping SUPP_VEC bits to tools)

Example. To run the script, use the following command:
```
python extract_sv_coordinates.py --vcf HG002_merged.vcf --output_prefix sv_output --supp_vec_map supp_vec_to_tool_map.json
```

Example of supp_vec_to_tool_map.json:
```
{
  "001": "delly",
  "010": "manta",
  "100": "smoove"
}
```

Output:
A BED file will be created for each tool, named like: sv_output_delly.bed, sv_output_manta.bed, sv_output_smoove.bed.

Notes:
The script assumes the presence of a SUPP_VEC field in the VCF file.
Ensure the supp_vec_to_tool_map.json file is formatted correctly as shown above.

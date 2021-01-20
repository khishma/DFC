# DFC
This github repository is created in context of the DFC contest 2021 under track "Multitemporal Semantic Change Detection" (MSD).  
The dataset is over the state of Maryland (USA) having 2250 tiles of 4000 x 4000 pixels collected in 2013 and 2017.
The baseline code has been developed from the paper: https://arxiv.org/pdf/2101.01154.pdf

The dataloaders scripts used to run the tiles NAIP datasets are as follows:

def __init__(self, imagery_fns, label_fns=None, groups=None, chip_size=256, num_chips_per_tile=200, windowed_sampling=False, image_transform=None, label_transform=None, nodata_check=None, verbose=False):

        """A torch Dataset for randomly sampling chips from a list of tiles. When used in conjunction with a DataLoader that has `num_workers>1` this Dataset will assign each worker to sample chips from disjoint sets of tiles.
        
        Args:
            imagery_fns: A list of filenames (or URLS -- anything that `rasterio.open()` can read) pointing to imagery tiles.
            label_fns: A list of filenames of the same size as `imagery_fns` pointing to label mask tiles or `None` if the Dataset should operate in "imagery only mode". Note that             we expect `imagery_fns[i]` and `label_fns[i]` to have the same dimension and coordinate system.
            groups: Optional: A list of integers of the same size as `imagery_fns` that gives the "group" membership of each tile. This can be used to normalize imagery from                   different groups differently.
            chip_size: Desired size of chips (in pixels).
            num_chips_per_tile: Desired number of chips to sample for each tile.
            windowed_sampling: Flag indicating whether we should sample each chip with a read using `rasterio.windows.Window` or whether we should read the whole tile into memory,             then sample chips.
            image_transform: A function to apply to each image chip object. If this is `None`, then the only transformation applied to the loaded imagery will be to convert it to             a `torch.Tensor`. If this is not `None`, then the function should return a `Torch.tensor`. Further, if `groups` is not `None` then the transform function should                    expect the imagery as the first argument and the group as the second argument.
            label_transform: Similar to image_transform, but applied to label chips.
            nodata_check: A method that will check an `(image_chip)` or `(image_chip, label_chip)` (if `label_fns` are provided) and return whether or not the chip should be                   skipped. This can be used, for example, to skip chips that contain nodata values.
            verbose: If `False` we will be quiet.
        """

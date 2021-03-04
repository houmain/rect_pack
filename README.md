# pack_rect

A small library for packing rectangles to one or more sprite sheets/atlases with optional constraints.

It is part of the [spright](https://github.com/houmain/spright) project and utilizing Sean T. Barrett's [Skyline](https://github.com/nothings/stb) and  Jukka Jylänki's [MaxRects](https://github.com/juj/RectangleBinPack) packing algorithm implementations.

Simply pass the desired settings and rectangle sizes to the _pack_ function. It will return one or more sheets containing the rectangles' positions. The id can be used to correlate in- and output (there is no rectangle for sizes which did not fit).

## Header

```cpp
#include <vector>

namespace rect_pack {

enum class Method {
  Best,
  Best_Skyline,
  Best_MaxRects,
  Skyline_BottomLeft,
  Skyline_BestFit,
  MaxRects_BestShortSideFit,
  MaxRects_BestLongSideFit,
  MaxRects_BestAreaFit,
  MaxRects_BottomLeftRule,
  MaxRects_ContactPointRule
};

struct Size {
  int id;
  int width;
  int height;
};

struct Rect {
  int id;
  int x;
  int y;
  int width;
  int height;
  bool rotated;
};

struct Sheet {
  int width;
  int height;
  std::vector<Rect> rects;
};

struct Settings {
  Method method;
  int max_sheets;
  bool power_of_two;
  bool square;
  bool allow_rotate;
  int align_width;
  int border_padding;
  int over_allocate;
  int min_width;
  int min_height;
  int max_width;
  int max_height;
};

std::vector<Sheet> pack(Settings settings, std::vector<Size> sizes);

} // namespace
```
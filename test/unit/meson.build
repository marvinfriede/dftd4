# This file is part of dftd4.
# SPDX-Identifier: LGPL-3.0-or-later
#
# dftd4 is free software: you can redistribute it and/or modify it under
# the terms of the Lesser GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# dftd4 is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# Lesser GNU General Public License for more details.
#
# You should have received a copy of the Lesser GNU General Public License
# along with dftd4.  If not, see <https://www.gnu.org/licenses/>.

# Create mstore as subproject for testing
mstore_dep = dependency(
  'mstore',
  version: '>=0.3.0',
  fallback: ['mstore', 'mstore_dep'],
  default_options: ['default_library=static'],
  required: not meson.is_subproject(),
)
# If we do not find mstore and are a subproject, we just skip testing
if not mstore_dep.found()
  subdir_done()
endif

tests = [
  'model',
  'dftd4',
  'pairwise',
  'param',
  'periodic',
]

test_srcs = files(
  'main.f90',
)
foreach t : tests
  test_srcs += files('test_@0@.f90'.format(t.underscorify()))
endforeach

tester = executable(
  'tester',
  sources: test_srcs,
  dependencies: [dftd4_dep, mstore_dep],
  link_language: 'fortran',
)

foreach t : tests
  test(t, tester, args: t)
endforeach

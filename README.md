# workbook-release

[![GitHub issues](https://img.shields.io/github/issues/iu-actions/workbook-release)](https://github.com/iu-actions/workbook-release/issues)

This action releases an IU Workbook.

## Found a bug? 💁‍♀️

Thanks for letting us know! Please [file an issue](../../issues/new?assignees=&labels=&template=bug_report.md&title=) and we should reply shortly.

## Configuration

This action requires the presence of inputs, which are listed below.

> **Note**: This action is dependent on the [iu-actions/workbook-cover](https://github.com/iu-actions/workbook-cover), [iu-actions/workbook-content](https://github.com/iu-actions/workbook-content) and [iu-actions/workbook-merge](https://github.com/iu-actions/workbook-merge) actions.

### Inputs
- `first_name`: The first name of the publishing student. (**required**)
- `last_name`: The last name of the publishing student. (**required**)
- `id`: The id of the publishing student. (**required**)

- `course_name`: The name of the course. (**required**)
- `course_id`: The id/number of the course. (**required**)

## Example

Below you will find an example of how you can use this action.

```yaml
jobs:
  cover:
    runs-on: ubuntu-latest
    steps:
      - name: Create Cover
        uses: iu-actions/workbook-cover@main
        with:
          # student details
          first_name: John
          last_name: Doe
          email: john.doe@university.edu
          id: 123456
          degree: B. Sc. Computer Science

          # course details
          course_name: Mathematics I
          course_id: 56.05J
          professor: Prof. Dr. John Doe
          tutor: Jane Doe

          # configuration details
          format_doc: .workbook/cover/format.docx
          template_doc: .workbook/cover/template.md
  content:
    runs-on: ubuntu-latest
    steps:
      - name: Create Content
        uses: iu-actions/workbook-content@main
        with:
          # workbook details
          workbook: exam/workbook.md

          # configuration details
          format_doc: .workbook/content/format.docx
  merge:
    needs: [cover, content]
    runs-on: ubuntu-latest
    steps:
      - name: Merge (Cover, Content)
        uses: iu-actions/workbook-merge@main
  release:
    needs: merge
    runs-on: ubuntu-latest
    steps:
      - name: Release Workbook
        uses: iu-actions/workbook-release@main
        with:
          # student details
          first_name: John
          last_name: Doe
          id: 123456

          # course details
          course_name: Mathematics I
          course_id: 56.05J
  ```

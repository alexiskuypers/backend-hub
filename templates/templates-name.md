# Templates de nommage Python

## Fonctions de transformation

```text
normalize_<thing>()
clean_<thing>()
format_<thing>()
parse_<thing>()
convert_<source>_to_<target>()
```

Exemples :

```python
normalize_title()
clean_email()
format_report()
parse_date()
convert_csv_row_to_book()
```

## Fonctions de validation

```text
is_<thing>_valid()
validate_<thing>()
has_<required_thing>()
can_<action>()
```

Exemples :

```python
is_status_valid()
validate_book()
has_required_fields()
can_borrow_book()
```

## Fonctions de construction

```text
build_<thing>()
create_<thing>()
make_<thing>()
```

Exemples :

```python
build_error()
build_summary()
create_book_record()
make_report_row()
```

## Fonctions de recherche / sélection

```text
find_<thing>_by_<key>()
get_<thing>()
keep_<condition>_<things>()
filter_<things>_by_<condition>()
remove_<condition>_<things>()
```

Exemples :

```python
find_book_by_id()
get_available_books()
keep_valid_books()
filter_books_by_status()
remove_empty_titles()
```

## Fonctions I/O

```text
read_<thing>()
write_<thing>()
load_<thing>()
save_<thing>()
show_<thing>()
ask_<thing>()
send_<thing>()
```

Exemples :

```python
read_books()
write_report()
load_config()
save_summary()
show_result()
ask_user_name()
send_email()
```

## Fonctions d’orchestration

```text
run()
run_<flow>()
process_<thing>()
execute_<workflow>()
handle_<command>()
```

Exemples :

```python
run()
run_import_flow()
process_books()
execute_validation_workflow()
handle_validate_command()
```

## Variables

```text
<thing>
raw_<thing>
normalized_<thing>
parsed_<thing>
valid_<things>
invalid_<things>
<thing>_by_<key>
```

Exemples :

```python
book
raw_title
normalized_title
parsed_date
valid_books
invalid_books
book_by_id
```

## Booléens

```text
is_<state>
has_<thing>
can_<action>
should_<action>
```

Exemples :

```python
is_valid
is_available
has_errors
has_required_fields
can_borrow
should_retry
```

## Modules

```text
<domain>.py
<responsibility>.py
```

Exemples :

```text
books.py
loans.py
reports.py
validators.py
normalizers.py
readers.py
writers.py
config.py
```

À éviter au début :

```text
utils.py
helpers.py
stuff.py
tools.py
misc.py
```
